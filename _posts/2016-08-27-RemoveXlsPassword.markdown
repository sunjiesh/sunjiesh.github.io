---
layout: post
title:  "去除Xls文件密码脚本"
date:   2016-08-27 12:05:00 +0800
categories: .Net
---

网上找了一下Office宏脚本，验证可行，进行收藏。

<pre>
Public Sub 工作表保护密码破解()
Const DBLSPACE As String = vbNewLine & vbNewLine
Const AUTHORS As String = DBLSPACE & vbNewLine & _
"作者:McCormick   JE McGimpsey "
Const HEADER As String = "工作表保护密码破解"
Const VERSION As String = DBLSPACE & "版本 Version 1.1.1"
Const REPBACK As String = DBLSPACE & ""
Const ZHENGLI As String = DBLSPACE & "                   hfhzi3—戊冥 整理"
Const ALLCLEAR As String = DBLSPACE & "该工作簿中的工作表密码保护已全部解除!!" & DBLSPACE & "请记得另保存" _
& DBLSPACE & "注意：不要用在不当地方，要尊重他人的劳动成果！"
Const MSGNOPWORDS1 As String = "该文件工作表中没有加密"
Const MSGNOPWORDS2 As String = "该文件工作表中没有加密2"
Const MSGTAKETIME As String = "解密需花费一定时间,请耐心等候!" & DBLSPACE & "按确定开始破解!"
Const MSGPWORDFOUND1 As String = "密码重新组合为:" & DBLSPACE & "$$" & DBLSPACE & _
"如果该文件工作表有不同密码,将搜索下一组密码并修改清除"
Const MSGPWORDFOUND2 As String = "密码重新组合为:" & DBLSPACE & "$$" & DBLSPACE & _
"如果该文件工作表有不同密码,将搜索下一组密码并解除"
Const MSGONLYONE As String = "确保为唯一的?"
Dim w1 As Worksheet, w2 As Worksheet
Dim i As Integer, j As Integer, k As Integer, l As Integer
Dim m As Integer, n As Integer, i1 As Integer, i2 As Integer
Dim i3 As Integer, i4 As Integer, i5 As Integer, i6 As Integer
Dim PWord1 As String
Dim ShTag As Boolean, WinTag As Boolean
Application.ScreenUpdating = False
With ActiveWorkbook
WinTag = .ProtectStructure Or .ProtectWindows
End With
ShTag = False
For Each w1 In Worksheets
ShTag = ShTag Or w1.ProtectContents
Next w1
If Not ShTag And Not WinTag Then
MsgBox MSGNOPWORDS1, vbInformation, HEADER
Exit Sub
End If
MsgBox MSGTAKETIME, vbInformation, HEADER
If Not WinTag Then
Else
On Error Resume Next
Do 'dummy do loop
For i = 65 To 66: For j = 65 To 66: For k = 65 To 66
For l = 65 To 66: For m = 65 To 66: For i1 = 65 To 66
For i2 = 65 To 66: For i3 = 65 To 66: For i4 = 65 To 66
For i5 = 65 To 66: For i6 = 65 To 66: For n = 32 To 126
With ActiveWorkbook
.Unprotect Chr(i) & Chr(j) & Chr(k) & _
Chr(l) & Chr(m) & Chr(i1) & Chr(i2) & _
Chr(i3) & Chr(i4) & Chr(i5) & Chr(i6) & Chr(n)
If .ProtectStructure = False And _
.ProtectWindows = False Then
PWord1 = Chr(i) & Chr(j) & Chr(k) & Chr(l) & _
Chr(m) & Chr(i1) & Chr(i2) & Chr(i3) & _
Chr(i4) & Chr(i5) & Chr(i6) & Chr(n)
MsgBox Application.Substitute(MSGPWORDFOUND1, _
"$$", PWord1), vbInformation, HEADER
Exit Do 'Bypass all for...nexts
End If
End With
Next: Next: Next: Next: Next: Next
Next: Next: Next: Next: Next: Next
Loop Until True
On Error GoTo 0
End If

If WinTag And Not ShTag Then
MsgBox MSGONLYONE, vbInformation, HEADER
Exit Sub
End If
On Error Resume Next

For Each w1 In Worksheets
'Attempt clearance with PWord1
w1.Unprotect PWord1
Next w1
On Error GoTo 0
ShTag = False
For Each w1 In Worksheets
'Checks for all clear ShTag triggered to 1 if not.
ShTag = ShTag Or w1.ProtectContents
Next w1
If ShTag Then
For Each w1 In Worksheets
With w1
If .ProtectContents Then
On Error Resume Next
Do 'Dummy do loop
For i = 65 To 66: For j = 65 To 66: For k = 65 To 66
For l = 65 To 66: For m = 65 To 66: For i1 = 65 To 66
For i2 = 65 To 66: For i3 = 65 To 66: For i4 = 65 To 66
For i5 = 65 To 66: For i6 = 65 To 66: For n = 32 To 126
.Unprotect Chr(i) & Chr(j) & Chr(k) & _
Chr(l) & Chr(m) & Chr(i1) & Chr(i2) & Chr(i3) & _
Chr(i4) & Chr(i5) & Chr(i6) & Chr(n)
If Not .ProtectContents Then
PWord1 = Chr(i) & Chr(j) & Chr(k) & Chr(l) & _
Chr(m) & Chr(i1) & Chr(i2) & Chr(i3) & _
Chr(i4) & Chr(i5) & Chr(i6) & Chr(n)
MsgBox Application.Substitute(MSGPWORDFOUND2, _
"$$", PWord1), vbInformation, HEADER
'leverage finding Pword by trying on other sheets
For Each w2 In Worksheets
w2.Unprotect PWord1
Next w2
Exit Do 'Bypass all for...nexts
End If
Next: Next: Next: Next: Next: Next
Next: Next: Next: Next: Next: Next
Loop Until True
On Error GoTo 0
End If
End With
Next w1
End If
MsgBox ALLCLEAR & AUTHORS & VERSION & REPBACK & ZHENGLI, vbInformation, HEADER
End Sub
</pre>

引用：
<a href="http://jingyan.baidu.com/article/20095761709405cb0721b4ef.html" target="_blank">http://jingyan.baidu.com/article/20095761709405cb0721b4ef.html</a>
