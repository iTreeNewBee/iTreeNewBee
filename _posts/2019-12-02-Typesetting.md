---
layout: post
title:  "vba实现文档排版"
date:   2019-12-02 11:00:00
categories: vba
tags: vba 宏
excerpt: 使用vba对word进行格式定制
---
* content
{:toc}  

## 需求
对开庭笔录进行特殊格式的定制,满足以下几个要求:
* 按照规定进行页面设置,包括页面大小,字体格式等等
* 首行缩进
* 去除所有空格和空行
* 前三段固定格式
* 特殊段落规定设置

## vba实现

```
Sub typeset()
'
' typeset 宏
'
'
'   清除格式
    Selection.WholeStory
    Selection.ClearParagraphDirectFormatting
    On Error Resume Next
    
'   首行缩进
    
    With Selection.ParagraphFormat
 
        .LeftIndent = CentimetersToPoints(0)
 
        .RightIndent = CentimetersToPoints(0)
 
        .SpaceBefore = 0
 
        .SpaceBeforeAuto = False
 
        .SpaceAfter = 0
 
        .SpaceAfterAuto = False
 
        .LineSpacingRule = wdLineSpaceSingle
 
        .Alignment = wdAlignParagraphJustify
 
        .WidowControl = False
 
        .KeepWithNext = False
 
        .KeepTogether = False
 
        .PageBreakBefore = False
 
        .NoLineNumber = False
 
        .Hyphenation = True
 
        .FirstLineIndent = CentimetersToPoints(0)
 
        .OutlineLevel = wdOutlineLevelBodyText
 
        .CharacterUnitLeftIndent = 0
 
        .CharacterUnitRightIndent = 0
 
        .CharacterUnitFirstLineIndent = 2
 
        .LineUnitBefore = 0
 
        .LineUnitAfter = 0
 
        .MirrorIndents = False
 
        .TextboxTightWrap = wdTightNone
 
        .AutoAdjustRightIndent = True
 
        .DisableLineHeightGrid = False
 
        .FarEastLineBreakControl = True
 
        .WordWrap = True
 
        .HangingPunctuation = True
 
        .HalfWidthPunctuationOnTopOfLine = False
 
        .AddSpaceBetweenFarEastAndAlpha = True
 
        .AddSpaceBetweenFarEastAndDigit = True
 
        .BaseLineAlignment = wdBaselineAlignAuto
 
    End With
    
    
'   清除段落前后空格
    For a = 1 To ActiveDocument.Paragraphs.Count
    Set sutRng = ActiveDocument.Paragraphs(a).Range
    sutRng.MoveEnd wdCharacter, -1
    sutRng.Text = Trim(sutRng.Text)
    sutRng.MoveEnd wdCharacter, 1
    ActiveDocument.Paragraphs(a).Range.Text = sutRng.Text
    Next a
    
'   清除空行，空格
    
    Dim i As Paragraph, n As Long
    Application.ScreenUpdating = False
    For Each i In ActiveDocument.Paragraphs
    If Len(i.Range) = 1 Then
    i.Range.Delete
    n = n + 1
    End If
    Selection.Find.ClearFormatting
    Selection.Find.Replacement.ClearFormatting
    With Selection.Find
    .Text = "　"
    .Replacement.Text = ""
    .Wrap = wdFindContinue
    End With
    With Selection.Find
    .Text = "vbTab"
    .Replacement.Text = ""
    .Wrap = wdFindContinue
    End With
    With Selection.Find
    .Text = " "
    .Replacement.Text = ""
    .Wrap = wdFindContinue
    End With
    With Selection.Find
        .Text = "^t"
        .Replacement.Text = ""
        .Forward = True
        .Wrap = wdFindContinue
        .Format = False
        .MatchCase = False
        .MatchWholeWord = False
        .MatchByte = True
        .MatchWildcards = False
        .MatchSoundsLike = False
        .MatchAllWordForms = False
    End With
    Selection.Find.Execute Replace:=wdReplaceAll
    Next
    Application.ScreenUpdating = True
    Options.AutoFormatAsYouTypeDeleteAutoSpaces = True
    Selection.Find.ClearFormatting
    Selection.Find.Replacement.ClearFormatting
    With Selection.Find
        .Text = " "
        .Replacement.Text = ""
        .Forward = True
        .Wrap = wdFindContinue
        .Format = False
        .MatchCase = False
        .MatchWholeWord = False
        .MatchByte = True
        .MatchWildcards = False
        .MatchSoundsLike = False
        .MatchAllWordForms = False
    End With
    Selection.Find.Execute Replace:=wdReplaceAll
    
    Selection.WholeStory
    With ActiveDocument.Styles(wdStyleNormal).Font
        If .NameFarEast = .NameAscii Then
            .NameAscii = ""
        End If
        .NameFarEast = ""
    End With
'   设置页面
    With Selection.PageSetup
        .LineNumbering.Active = False
        .Orientation = wdOrientPortrait
        .TopMargin = CentimetersToPoints(2.54)
        .BottomMargin = CentimetersToPoints(1.4)
        .LeftMargin = CentimetersToPoints(2.2)
        .RightMargin = CentimetersToPoints(1.3)
        .Gutter = CentimetersToPoints(0)
        .HeaderDistance = CentimetersToPoints(1.3)
        .FooterDistance = CentimetersToPoints(2)
        .PageWidth = CentimetersToPoints(21)
        .PageHeight = CentimetersToPoints(29.7)
        .FirstPageTray = wdPrinterDefaultBin
        .OtherPagesTray = wdPrinterDefaultBin
        .SectionStart = wdSectionNewPage
        .OddAndEvenPagesHeaderFooter = False
        .DifferentFirstPageHeaderFooter = False
        .VerticalAlignment = wdAlignVerticalTop
        .SuppressEndnotes = False
        .MirrorMargins = False
        .TwoPagesOnOne = False
        .BookFoldPrinting = False
        .BookFoldRevPrinting = False
        .BookFoldPrintingSheets = 1
        .GutterPos = wdGutterPosLeft
        .CharsLine = 39
        .LinesPage = 32
        .LayoutMode = wdLayoutModeGrid
    End With
    

        
'   设置段落
    If (ActiveDocument.Paragraphs.Count >= 1) Then
    ActiveWindow.ActivePane.View.SeekView = wdSeekMainDocument
    Selection.MoveLeft unit:=wdCharacter, Count:=1
    Selection.MoveDown unit:=wdParagraph, Count:=1, Extend:=wdExtend
    Selection.ParagraphFormat.Alignment = wdAlignParagraphCenter
    Selection.Font.Name = "宋体"
    Selection.Font.Bold = wdToggle
    Selection.Font.Size = 22
    Selection.MoveRight unit:=wdCharacter, Count:=1
    End If
    
    If (ActiveDocument.Paragraphs.Count >= 2) Then
    Selection.MoveDown unit:=wdParagraph, Count:=1, Extend:=wdExtend
    Selection.ParagraphFormat.Alignment = wdAlignParagraphCenter
    Selection.Font.Name = "宋体"
    Selection.Font.Bold = wdToggle
    Selection.Font.Size = 22
    Selection.MoveRight unit:=wdCharacter, Count:=1
    End If
    
    If (ActiveDocument.Paragraphs.Count >= 3) Then
    Selection.MoveDown unit:=wdParagraph, Count:=ActiveDocument.Paragraphs.Count - 2, Extend:=wdExtend
    Selection.Font.Name = "GB2312"
    Selection.Font.Size = 16
    Selection.MoveRight unit:=wdCharacter, Count:=1
    End If
    
'   加空段落
    ActiveDocument.Paragraphs(2).Range.InsertAfter Chr(13)

'   关键字居中或加粗
    Dim arr_sum(), arr(14), m As Integer, q
    arr(0) = "宣布法庭纪律"
    arr(1) = "宣布开庭"
    arr(2) = "法庭调查"
    arr(3) = "最后陈述"
    arr(4) = "法庭调解"
    arr(5) = "当庭宣判"
    arr(6) = "宣布法庭组成人员和书记员名单"
    arr(7) = "宣布法庭组成人员和书记员名单"
    arr(8) = "告知当事人有关的诉讼权利和义务"
    arr(9) = "诉称部分"
    arr(10) = "答辩部分"
    arr(11) = "法庭归纳争议焦点"
    arr(12) = "当事人举证质证部分"
    arr(13) = "原告举证部分"
    arr(14) = "被告举证部分"
    For m = 0 To 14
    Selection.Find.ClearFormatting
    With Selection.Find
        .Text = arr(m)
        .Replacement.Text = ""
        .Format = True
        .Wrap = wdFindContinue
        .Format = False
        .MatchCase = False
        .MatchWholeWord = False
        .MatchByte = True
        .MatchWildcards = False
        .MatchWildcards = False
        .MatchSoundsLike = False
        .MatchAllWordForms = False
    End With
    
    s = ActiveDocument.Range(0, Selection.End).Paragraphs.Count
    q = ActiveDocument.Paragraphs(s).Range.Characters.Count
    Selection.Find.Execute
    If Selection.Font.Bold = False Then
        Selection.Font.Bold = wdToggle
    End If
    If m <= 5 Then
    Selection.Font.Size = 18
    Selection.ParagraphFormat.Alignment = wdAlignParagraphCenter
    End If
    
  
    Next
    
    
'   案由，案号替换格式
    
    Set myRangeb = ActiveDocument.Content
    myRangeb.Find.ClearFormatting
    Dim b As Long
    b = myRangeb.End
    Do While myRangeb.Find.Execute("案号")
    myRangeb.Select
    myRangeb.Text = "案    号"
    myRangeb.Start = myRangeb.Start + Len(myRangeb.Find.Text)
    myRangeb.End = b
    Loop
        
    
    
    
    Set myRangea = ActiveDocument.Content
    myRangea.Find.ClearFormatting
    Dim f As Long
    f = myRangea.End
    Do While myRangea.Find.Execute("案由")
    myRangea.Select
    myRangea.Text = "案    由"
    myRangea.Start = myRangea.Start + Len(myRangea.Find.Text)
    myRangea.End = f
    Loop
    
'   关键字用缩进方式对齐
    Dim arr2(7), j As Integer
    arr2(0) = "人民陪审员："
    arr2(1) = "审判员："
    arr2(2) = "书记员："
    arr2(3) = "有无间断："
    arr2(4) = "其他说明："
    arr2(5) = "结束时间："
    arr2(6) = "原告方："
    arr2(7) = "被告方："
    For j = 0 To 7
    Selection.Find.ClearFormatting
    With Selection.Find
        .Text = arr2(j)
        .Replacement.Text = ""
        .Format = True
        .Wrap = wdFindContinue
        .Format = False
        .MatchCase = False
        .MatchWholeWord = False
        .MatchByte = True
        .MatchWildcards = False
        .MatchWildcards = False
        .MatchSoundsLike = False
        .MatchAllWordForms = False
    End With
    Selection.Find.Execute
    Selection.ParagraphFormat.Alignment = wdAlignParagraphLeft
    Selection.ParagraphFormat.LeftIndent = 165
    If j <= 2 Then
    Selection.ParagraphFormat.LeftIndent = 110
    End If
    If j > 5 Then
    Selection.ParagraphFormat.LeftIndent = 330
    End If
    Next
    

End Sub
```