---
title: "Excel VBA セル内の文字列のチェックと変換"
date: 2009-07-06T11:49:00+09:00
archives: ["2009-07"]
draft: false
categories: ['SOURCE LIBRARY']

---

WordPressのプラグインで、WP-Syntaxっていうソースコードを整形して表示するものがあります。
これならいちいちHTMLタグやエスケープシーケンスを入れずに済むのでサンプルを公開しやすくなるかな。

このコードは実際に動きます。

Excelのマクロでコード編集を表示して貼り付けてください。
後はシートにボタンを貼り付けて、先頭の２つのプロシージャーを呼び出せばＯＫです。
中に"N2S"という関数がありますが、Nullチェックをしています。
何か作って置き換えてください。


```vbnet {.copy}
Option Explicit

'定数
Public Const COMMAND_CHECKCELL_WIDEALPHABET = 1
Public Const COMMAND_CHECKCELL_WIDENUMBERS = 2
Public Const COMMAND_CHECKCELL_WIDEMARKS = 3
Public Const COMMAND_CHECKCELL_WIDECOMMA = 4
Public Const COMMAND_CHECKCELL_WITHOUTINCLUDEDCHAR = 5

Public Const COMMAND_CONVERT_WIDEALPHABET = 1
Public Const COMMAND_CONVERT_WIDENUMBERS = 2
Public Const COMMAND_CONVERT_WIDEMARKS = 3
Public Const COMMAND_CONVERT_WIDECOMMA = 4

'色
Public Const COLOR_PINK = 16711935
Public Const COLOR_BLUE = 16776960

'セルのフォント情報の保存
'メンバーは何が入ってくるかわからないのでとりあえず「Variant」
Type tyFontInfo
    vBold As Variant
    vColor As Variant
    vColorIndex As Variant
    vFontStyle As Variant
    vItalic As Variant
    vName As Variant
    vShadow As Variant
    vSize As Variant
    vStrikethrough As Variant
    vSubscript As Variant
    vSuperscript As Variant
    vUnderline As Variant
End Type

'イベント共通処理
'チェック
Public Function gExecCellCheck(ByVal lCommand As Long) As Boolean
    On Error GoTo ErrProc

    Dim lRow As Long
    Dim lCol As Long
    Dim objWs As Excel.Worksheet

    Set objWs = Application.ThisWorkbook.ActiveSheet
    lRow = Application.ActiveCell.Row
    lCol = Application.ActiveCell.Column
    Application.ScreenUpdating = False
    
    Select Case lCommand
        Case COMMAND_CHECKCELL_WIDEALPHABET, _
             COMMAND_CHECKCELL_WIDENUMBERS, _
             COMMAND_CHECKCELL_WIDEMARKS, _
             COMMAND_CHECKCELL_WIDECOMMA
            If CheckCell_WideThin(objWs, lRow, lCol, lCommand) Then
            Else
                'チェック対象が見つからなかった
            End If
            
        Case COMMAND_CHECKCELL_WITHOUTINCLUDEDCHAR
            If CheckCell_WithOutIncludedChar(objWs, lRow, lCol) Then
            End If
            
        Case Else
        
    End Select
    
    Application.ScreenUpdating = True
    MsgBox "チェック終了", vbOKOnly + vbInformation
ExitProc:
    Exit Function
ErrProc:
    Call ErrFunc(Err, "gExecCellCheck")
    Resume ExitProc
End Function

'イベント共通処理
'変換
Public Function gExecCellConvert(ByVal lCommand As Long) As Boolean
    On Error GoTo ErrProc

    Dim lRow As Long
    Dim lCol As Long
    Dim objWs As Excel.Worksheet

    If vbYes = MsgBox("変換処理をすると元に戻すことができません。" & vbCrLf & _
                      "事前にバックアップを作ることを推奨します。" & vbCrLf & vbCrLf & _
                      "変換処理を行いますか？", vbYesNo + vbQuestion) Then
    Else
        GoTo ExitProc
    End If
    Application.ScreenUpdating = False
    
    Set objWs = Application.ThisWorkbook.ActiveSheet
    lRow = Application.ActiveCell.Row
    lCol = Application.ActiveCell.Column
   
    If Convert_Letter(objWs, lRow, lCol, lCommand) Then
        MsgBox "変換終了", vbOKOnly + vbInformation
    Else
        '変換の失敗
        MsgBox "変換できませんでした。", vbOKOnly + vbExclamation
    End If
    
ExitProc:
    Application.ScreenUpdating = True
    Exit Function
ErrProc:
    Call ErrFunc(Err, "gExecCellConvert")
    Resume ExitProc
End Function

'選択中のセルの書式を保存した後、変更
Private Function CheckCell_WithOutIncludedChar(ByVal objWs As Excel.Worksheet, _
                                               ByVal lRow As Long, _
                                               ByVal lCol As Long) As Boolean
    CheckCell_WithOutIncludedChar = False
    On Error GoTo ErrProc
    
    Dim strCellValue As String
    Dim lCnt As Long
    Dim arrErrStringIdx() As Long
    
    ReDim arrErrStringIdx(0)
    
    strCellValue = objWs.Cells(lRow, lCol).value
    If CheckLetter_WithOut_OSIncluded(strCellValue, arrErrStringIdx) Then
    Else
        For lCnt = 0 To UBound(arrErrStringIdx)
            If objWs.Cells(lRow, lCol).Characters(arrErrStringIdx(lCnt), 1).Font.Color = COLOR_PINK Then
                objWs.Cells(lRow, lCol).Characters(arrErrStringIdx(lCnt), 1).Font.Color = 0
            ElseIf objWs.Cells(lRow, lCol).Characters(arrErrStringIdx(lCnt), 1).Font.Color = 0 Then
                objWs.Cells(lRow, lCol).Characters(arrErrStringIdx(lCnt), 1).Font.Color = COLOR_PINK
            Else
            End If
            CheckCell_WithOutIncludedChar = True
        Next
    End If
    
ExitProc:
    Exit Function
ErrProc:
    Call ErrFunc(Err, "CheckCell_WithOutIncludedChar")
    Resume ExitProc
End Function

'機種依存文字以外のチェック
Private Function CheckCell_WideThin(ByVal objWs As Excel.Worksheet, _
                                    ByVal lRow As Long, _
                                    ByVal lCol As Long, _
                                    ByVal lMode As Long) As Boolean
    CheckCell_WideThin = False
    On Error GoTo ErrProc
    
    Dim strCellValue As String
    Dim lCnt As Long
    Dim arrWideStringIdx() As Long
    Dim arrThinStringIdx() As Long
    Dim flgCheckOK As Boolean
    
    strCellValue = objWs.Cells(lRow, lCol).value
    
    Select Case lMode
        Case COMMAND_CHECKCELL_WIDEALPHABET
            flgCheckOK = Check_WideToThin_Alphabet(strCellValue, arrWideStringIdx, arrThinStringIdx)
        Case COMMAND_CHECKCELL_WIDENUMBERS
            flgCheckOK = Check_WideToThin_Numeric(strCellValue, arrWideStringIdx, arrThinStringIdx)
        Case COMMAND_CHECKCELL_WIDEMARKS
            flgCheckOK = Check_WideToThin_Mark(strCellValue, arrWideStringIdx, arrThinStringIdx)
        Case COMMAND_CHECKCELL_WIDECOMMA
            flgCheckOK = Check_WideToThin_Comma(strCellValue, arrWideStringIdx, arrThinStringIdx)
        Case Else
        
    End Select
    
    If flgCheckOK Then
    Else
        GoTo ExitProc
    End If
    
    '全角チェック
    For lCnt = 0 To UBound(arrWideStringIdx)
        If objWs.Cells(lRow, lCol).Characters(arrWideStringIdx(lCnt), 1).Font.Color = COLOR_PINK Then
            objWs.Cells(lRow, lCol).Characters(arrWideStringIdx(lCnt), 1).Font.Color = 0
        ElseIf objWs.Cells(lRow, lCol).Characters(arrWideStringIdx(lCnt), 1).Font.Color = 0 Then
            objWs.Cells(lRow, lCol).Characters(arrWideStringIdx(lCnt), 1).Font.Color = COLOR_PINK
        Else
        End If
    Next
    '半角チェック
    For lCnt = 0 To UBound(arrThinStringIdx)
        If objWs.Cells(lRow, lCol).Characters(arrThinStringIdx(lCnt), 1).Font.Color = COLOR_BLUE Then
            objWs.Cells(lRow, lCol).Characters(arrThinStringIdx(lCnt), 1).Font.Color = 0
        ElseIf objWs.Cells(lRow, lCol).Characters(arrThinStringIdx(lCnt), 1).Font.Color = 0 Then
            objWs.Cells(lRow, lCol).Characters(arrThinStringIdx(lCnt), 1).Font.Color = COLOR_BLUE
        Else
        End If
    Next
    
    CheckCell_WideThin = True
    
ExitProc:
    Exit Function
ErrProc:
    Call ErrFunc(Err, "CheckCell_WideThin")
    Resume ExitProc
End Function

'機種依存文字の判別
'機種依存文字のインデックスを返す。
Private Function CheckLetter_WithOut_OSIncluded(ByVal strCheck As String, _
                                                ByRef arrErrStringIdx() As Long) As Boolean
    CheckLetter_WithOut_OSIncluded = False
    
    Dim lCheckLength As Long
    Dim lCharacter As Long
    Dim lIdx As Long
    Dim lCnt As Long
    
    On Error GoTo ErrProc
    
    lCheckLength = Len(strCheck)
    
    lCnt = 0                        'カウンターをリセット
    lIdx = 0                        '配列のインデックスをリセット
    ReDim arrErrStringIdx(lIdx)     '配列をリセット
    
'   Excelの"Asc"はSignedで正負を含む10進数を返します。
'   1:NEC選定特殊文字   -30823 ～ -30912
'   2:IBM選定特殊文字   -1472 ～ -949
    For lCnt = 1 To lCheckLength
        lCharacter = Asc(Mid(strCheck, lCnt, 1))
        If (lCharacter <= -30823 And lCharacter >= -30912) Or (lCharacter <= -949 And lCharacter >= -1472) Then
            ReDim Preserve arrErrStringIdx(lIdx)    '配列をリセット
            arrErrStringIdx(lIdx) = lCnt            '配列に機種依存文字のインデックスをセット[～文字目]
            lIdx = lIdx + 1
        End If
    Next
    
    If lIdx > 0 Then
        CheckLetter_WithOut_OSIncluded = False
    Else
        CheckLetter_WithOut_OSIncluded = True
    End If
ExitProc:
    Exit Function
ErrProc:
    Call ErrFunc(Err, "CheckLetter_WithOut_OSIncluded")
    Resume ExitProc
End Function

'アルファベットチェック
Private Function Check_WideToThin_Alphabet(ByVal strCheck As String, _
                                           ByRef arrWideStringIdx() As Long, _
                                           ByRef arrThinStringIdx() As Long) As Boolean
    Check_WideToThin_Alphabet = False
    On Error GoTo ErrProc
    
    Dim lCheckLength As Long
    Dim lCharacter As Long
    Dim lWideIdx As Long
    Dim lThinIdx As Long
    Dim lCnt As Long
    
    lCheckLength = Len(strCheck)
    lCnt = 0
    lWideIdx = 0
    lThinIdx = 0
    ReDim arrWideStringIdx(lWideIdx)
    ReDim arrThinStringIdx(lThinIdx)
    
    'A:65～Z:90/a:97～z:122
    'Ａ:-32160～Ｚ:-32135/ａ:-32127～ｚ:-32102
    For lCnt = 1 To lCheckLength
        lCharacter = Asc(Mid(strCheck, lCnt, 1))
        If (lCharacter <= 90 And lCharacter >= 65) Or (lCharacter <= 122 And lCharacter >= 97) Then
            ReDim Preserve arrThinStringIdx(lThinIdx)    '配列をリセット
            arrThinStringIdx(lThinIdx) = lCnt            '配列に半角英字のインデックスをセット[～文字目]
            lThinIdx = lThinIdx + 1
            Check_WideToThin_Alphabet = True
        End If
        If (lCharacter <= -32135 And lCharacter >= -32160) Or (lCharacter <= -32102 And lCharacter >= -32127) Then
            ReDim Preserve arrWideStringIdx(lWideIdx)    '配列をリセット
            arrWideStringIdx(lWideIdx) = lCnt            '配列に全角英字のインデックスをセット[～文字目]
            lWideIdx = lWideIdx + 1
            Check_WideToThin_Alphabet = True
        End If
    Next
ExitProc:
    Exit Function
ErrProc:
    Call ErrFunc(Err, "Check_WideToThin_Alphabet")
    Resume ExitProc
End Function

'数字チェック
Private Function Check_WideToThin_Numeric(ByVal strCheck As String, _
                                          ByRef arrWideStringIdx() As Long, _
                                          ByRef arrThinStringIdx() As Long) As Boolean
    Check_WideToThin_Numeric = False
    On Error GoTo ErrProc
        
    Dim lCheckLength As Long
    Dim lCharacter As Long
    Dim lWideIdx As Long
    Dim lThinIdx As Long
    Dim lCnt As Long
    
    lCheckLength = Len(strCheck)
    lCnt = 0
    lWideIdx = 0
    lThinIdx = 0
    ReDim arrWideStringIdx(lWideIdx)
    ReDim arrThinStringIdx(lThinIdx)
    
    '0:48～9:57
    '０:-32177～９:-32168
    For lCnt = 1 To lCheckLength
        lCharacter = Asc(Mid(strCheck, lCnt, 1))
        If lCharacter <= 57 And lCharacter >= 48 Then
            ReDim Preserve arrThinStringIdx(lThinIdx)    '配列をリセット
            arrThinStringIdx(lThinIdx) = lCnt            '配列に半角数字のインデックスをセット[～文字目]
            lThinIdx = lThinIdx + 1
            Check_WideToThin_Numeric = True
        End If
        If lCharacter <= -32168 And lCharacter >= -32177 Then
            ReDim Preserve arrWideStringIdx(lWideIdx)    '配列をリセット
            arrWideStringIdx(lWideIdx) = lCnt            '配列に全角数字のインデックスをセット[～文字目]
            lWideIdx = lWideIdx + 1
            Check_WideToThin_Numeric = True
        End If
    Next
    
ExitProc:
    Exit Function
ErrProc:
    Call ErrFunc(Err, "Check_WideToThin_Numeric")
    Resume ExitProc
End Function

'記号チェック
Private Function Check_WideToThin_Mark(ByVal strCheck As String, _
                                       ByRef arrWideStringIdx() As Long, _
                                       ByRef arrThinStringIdx() As Long) As Boolean
    Check_WideToThin_Mark = False
    On Error GoTo ErrProc
        
    Dim lCheckLength As Long
    Dim lCharacter As Long
    Dim lWideIdx As Long
    Dim lThinIdx As Long
    Dim lCnt As Long
    
    lCheckLength = Len(strCheck)
    lCnt = 0
    lWideIdx = 0
    lThinIdx = 0
    ReDim arrWideStringIdx(lWideIdx)
    ReDim arrThinStringIdx(lThinIdx)
    
    '+,-,*,=
    '＋,－,＊,＝
    For lCnt = 1 To lCheckLength
        lCharacter = Asc(Mid(strCheck, lCnt, 1))
        
        Select Case lCharacter
            
            Case 42, 43, 45, 61
                ReDim Preserve arrThinStringIdx(lThinIdx)    '配列をリセット
                arrThinStringIdx(lThinIdx) = lCnt            '配列に半角記号のインデックスをセット[～文字目]
                lThinIdx = lThinIdx + 1
                Check_WideToThin_Mark = True
            
            Case -32383, -32388, -32362, -32389
                ReDim Preserve arrWideStringIdx(lWideIdx)    '配列をリセット
                arrWideStringIdx(lWideIdx) = lCnt            '配列に全角記号のインデックスをセット[～文字目]
                lWideIdx = lWideIdx + 1
                Check_WideToThin_Mark = True
            
            Case Else
        
        End Select
        
    Next
    
ExitProc:
    Exit Function
ErrProc:
    Call ErrFunc(Err, "Check_WideToThin_Mark")
    Resume ExitProc
End Function

'カンマチェック
Private Function Check_WideToThin_Comma(ByVal strCheck As String, _
                                        ByRef arrWideStringIdx() As Long, _
                                        ByRef arrThinStringIdx() As Long) As Boolean
    Check_WideToThin_Comma = False
    
    On Error GoTo ErrProc
        
    Dim lCheckLength As Long
    Dim lCharacter As Long
    Dim lWideIdx As Long
    Dim lThinIdx As Long
    Dim lCnt As Long
    
    lCheckLength = Len(strCheck)
    lCnt = 0
    lWideIdx = 0
    lThinIdx = 0
    ReDim arrWideStringIdx(lWideIdx)
    ReDim arrThinStringIdx(lThinIdx)
    
    ',
    '、，
    For lCnt = 1 To lCheckLength
        lCharacter = Asc(Mid(strCheck, lCnt, 1))
        
        Select Case lCharacter
            
            Case 44
                ReDim Preserve arrThinStringIdx(lThinIdx)    '配列をリセット
                arrThinStringIdx(lThinIdx) = lCnt            '配列に半角カンマのインデックスをセット[～文字目]
                lThinIdx = lThinIdx + 1
                Check_WideToThin_Comma = True
            
            Case -32445, -32447
                ReDim Preserve arrWideStringIdx(lWideIdx)    '配列をリセット
                arrWideStringIdx(lWideIdx) = lCnt            '配列に全角カンマのインデックスをセット[～文字目]
                lWideIdx = lWideIdx + 1
                Check_WideToThin_Comma = True
            
            Case Else
        
        End Select
        
    Next

ExitProc:
    Exit Function
ErrProc:
    Call ErrFunc(Err, "Check_WideToThin_Comma")
    Resume ExitProc
End Function

'文字列変換
Private Function Convert_Letter(ByVal objWs As Excel.Worksheet, _
                                ByVal lRow As Long, _
                                ByVal lCol As Long, _
                                ByVal lMode As Long) As Boolean
                                
    Convert_Letter = False
    On Error GoTo ErrProc
    
    Dim strCellValue As String
    Dim lCnt As Long
    Dim lIdx As Long
    Dim arrWideStringIdx() As Long
    Dim arrThinStringIdx() As Long
    Dim strBuffer As String
    Dim strConvBuffer As String
    Dim lCellLength As Long
    Dim flgCheckOK As Boolean
    
    lCnt = 0
    lIdx = 0
    strConvBuffer = ""
    flgCheckOK = False
    
    ReDim arrErrStringIdx(0)
    
    Dim objFont() As tyFontInfo
    
    strCellValue = objWs.Cells(lRow, lCol).value
    lCellLength = Len(strCellValue)
    ReDim objFont(lCellLength - 1)
    
    Select Case lMode
        Case COMMAND_CONVERT_WIDEALPHABET
            flgCheckOK = Check_WideToThin_Alphabet(strCellValue, arrWideStringIdx, arrThinStringIdx)
        Case COMMAND_CONVERT_WIDENUMBERS
            flgCheckOK = Check_WideToThin_Numeric(strCellValue, arrWideStringIdx, arrThinStringIdx)
        Case COMMAND_CONVERT_WIDEMARKS
            flgCheckOK = Check_WideToThin_Mark(strCellValue, arrWideStringIdx, arrThinStringIdx)
        Case COMMAND_CONVERT_WIDECOMMA
            flgCheckOK = Check_WideToThin_Comma(strCellValue, arrWideStringIdx, arrThinStringIdx)
        Case Else
        
    End Select
    
    If flgCheckOK Then
    Else
        '終了する
        GoTo ExitProc
    End If
    
    For lCnt = 0 To lCellLength - 1
        '書式の保存
        With objWs.Cells(lRow, lCol).Characters(lCnt + 1, 1).Font
            objFont(lCnt).vBold = .Bold
            objFont(lCnt).vColor = .Color
            objFont(lCnt).vColorIndex = .ColorIndex
            objFont(lCnt).vFontStyle = .FontStyle
            objFont(lCnt).vItalic = .Italic
            objFont(lCnt).vName = .Name
            objFont(lCnt).vShadow = .Shadow
            objFont(lCnt).vSize = .Size
            objFont(lCnt).vStrikethrough = .Strikethrough
            objFont(lCnt).vSubscript = .Subscript
            objFont(lCnt).vSuperscript = .Superscript
            objFont(lCnt).vUnderline = .Underline
        End With

        strConvBuffer = Mid(strCellValue, lCnt + 1, 1)
        
        Select Case lMode
            Case COMMAND_CONVERT_WIDEALPHABET
                'アルファベットを全角から半角へ
                For lIdx = 0 To UBound(arrWideStringIdx)
                    If arrWideStringIdx(lIdx) = lCnt + 1 Then
                        strConvBuffer = StrConv(strConvBuffer, vbNarrow)
                    End If
                Next
            Case COMMAND_CONVERT_WIDENUMBERS
                '数字を全角から半角へ
                For lIdx = 0 To UBound(arrWideStringIdx)
                    If arrWideStringIdx(lIdx) = lCnt + 1 Then
                        strConvBuffer = StrConv(strConvBuffer, vbNarrow)
                    End If
                Next
            Case COMMAND_CONVERT_WIDEMARKS
                '記号を全角から半角へ
                For lIdx = 0 To UBound(arrWideStringIdx)
                    If arrWideStringIdx(lIdx) = lCnt + 1 Then
                        strConvBuffer = StrConv(strConvBuffer, vbNarrow)
                    End If
                Next
            Case COMMAND_CONVERT_WIDECOMMA
                'カンマをすべて全角の「，」へ
                For lIdx = 0 To UBound(arrWideStringIdx)
                    If arrWideStringIdx(lIdx) = lCnt + 1 Then
                        strConvBuffer = "，"
                    End If
                Next
                For lIdx = 0 To UBound(arrThinStringIdx)
                    If arrThinStringIdx(lIdx) = lCnt + 1 Then
                        strConvBuffer = "，"
                    End If
                Next
            Case Else
            
        End Select
        
        strBuffer = strBuffer & strConvBuffer
    Next
    
    '文字列をセルに
    objWs.Cells(lRow, lCol).value = strBuffer
    
    '書式を書き戻す
    For lCnt = 0 To lCellLength - 1
        With objWs.Cells(lRow, lCol).Characters(lCnt + 1, 1).Font
            .Bold = objFont(lCnt).vBold
            .Color = objFont(lCnt).vColor
            .ColorIndex = objFont(lCnt).vColorIndex
            .FontStyle = objFont(lCnt).vFontStyle
            .Italic = objFont(lCnt).vItalic
            .Name = objFont(lCnt).vName
            .Shadow = objFont(lCnt).vShadow
            .Size = objFont(lCnt).vSize
            .Strikethrough = objFont(lCnt).vStrikethrough
            .Subscript = objFont(lCnt).vSubscript
            .Superscript = objFont(lCnt).vSuperscript
            .Underline = objFont(lCnt).vUnderline
        End With
    Next
    
    Convert_Letter = True
ExitProc:
    Exit Function
ErrProc:
    Call ErrFunc(Err, "Convert_Letter")
    Resume ExitProc
End Function

```
