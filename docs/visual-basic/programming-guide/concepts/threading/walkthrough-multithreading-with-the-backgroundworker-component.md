---
title: "多執行緒處理和 BackgroundWorker 元件 (Visual Basic) |Microsoft 文件"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: e4cd9b2a-f924-470e-a16e-50274709b40e
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 88d0711c8e417ae5c95b0e109504b69882015241
ms.contentlocale: zh-tw
ms.lasthandoff: 04/12/2017

---
# <a name="walkthrough-multithreading-with-the-backgroundworker-component-visual-basic"></a><span data-ttu-id="649d4-102">逐步解說︰ 使用 BackgroundWorker 元件 (Visual Basic) 的多執行緒處理</span><span class="sxs-lookup"><span data-stu-id="649d4-102">Walkthrough: Multithreading with the BackgroundWorker Component (Visual Basic)</span></span>
<span data-ttu-id="649d4-103">本逐步解說示範如何建立多執行緒的 Windows Form 應用程式，以搜尋相符項目文字的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="649d4-103">This walkthrough demonstrates how to create a multithreaded Windows Forms application that searches a text file for occurrences of a word.</span></span> <span data-ttu-id="649d4-104">它會示範︰</span><span class="sxs-lookup"><span data-stu-id="649d4-104">It demonstrates:</span></span>  
  
-   <span data-ttu-id="649d4-105">定義類別的方法，可由呼叫<xref:System.ComponentModel.BackgroundWorker>元件。</xref:System.ComponentModel.BackgroundWorker></span><span class="sxs-lookup"><span data-stu-id="649d4-105">Defining a class with a method that can be called by the <xref:System.ComponentModel.BackgroundWorker> component.</span></span>  
  
-   <span data-ttu-id="649d4-106">處理所引發的事件<xref:System.ComponentModel.BackgroundWorker>元件。</xref:System.ComponentModel.BackgroundWorker></span><span class="sxs-lookup"><span data-stu-id="649d4-106">Handling events raised by the <xref:System.ComponentModel.BackgroundWorker> component.</span></span>  
  
-   <span data-ttu-id="649d4-107">啟動<xref:System.ComponentModel.BackgroundWorker>元件來執行方法。</xref:System.ComponentModel.BackgroundWorker></span><span class="sxs-lookup"><span data-stu-id="649d4-107">Starting a <xref:System.ComponentModel.BackgroundWorker> component to run a method.</span></span>  
  
-   <span data-ttu-id="649d4-108">實作`Cancel`停止按鈕<xref:System.ComponentModel.BackgroundWorker>元件。</xref:System.ComponentModel.BackgroundWorker></span><span class="sxs-lookup"><span data-stu-id="649d4-108">Implementing a `Cancel` button that stops the <xref:System.ComponentModel.BackgroundWorker> component.</span></span>  
  
### <a name="to-create-the-user-interface"></a><span data-ttu-id="649d4-109">若要建立使用者介面</span><span class="sxs-lookup"><span data-stu-id="649d4-109">To create the user interface</span></span>  
  
1.  <span data-ttu-id="649d4-110">開啟新的 Visual Basic Windows Form 應用程式專案，並建立名為的表單`Form1`。</span><span class="sxs-lookup"><span data-stu-id="649d4-110">Open a new Visual Basic Windows Forms Application project, and create a form named `Form1`.</span></span>  
  
2.  <span data-ttu-id="649d4-111">將兩個按鈕和四個文字方塊來加入`Form1`。</span><span class="sxs-lookup"><span data-stu-id="649d4-111">Add two buttons and four text boxes to `Form1`.</span></span>  
  
3.  <span data-ttu-id="649d4-112">下表所示，為物件命名。</span><span class="sxs-lookup"><span data-stu-id="649d4-112">Name the objects as shown in the following table.</span></span>  
  
    |<span data-ttu-id="649d4-113">物件</span><span class="sxs-lookup"><span data-stu-id="649d4-113">Object</span></span>|<span data-ttu-id="649d4-114">屬性</span><span class="sxs-lookup"><span data-stu-id="649d4-114">Property</span></span>|<span data-ttu-id="649d4-115">設定</span><span class="sxs-lookup"><span data-stu-id="649d4-115">Setting</span></span>|  
    |------------|--------------|-------------|  
    |<span data-ttu-id="649d4-116">第一個按鈕</span><span class="sxs-lookup"><span data-stu-id="649d4-116">First button</span></span>|<span data-ttu-id="649d4-117">`Name`, `Text`</span><span class="sxs-lookup"><span data-stu-id="649d4-117">`Name`, `Text`</span></span>|<span data-ttu-id="649d4-118">[開始] 開始</span><span class="sxs-lookup"><span data-stu-id="649d4-118">Start, Start</span></span>|  
    |<span data-ttu-id="649d4-119">第二個按鈕</span><span class="sxs-lookup"><span data-stu-id="649d4-119">Second button</span></span>|<span data-ttu-id="649d4-120">`Name`, `Text`</span><span class="sxs-lookup"><span data-stu-id="649d4-120">`Name`, `Text`</span></span>|<span data-ttu-id="649d4-121">[取消]，[取消]</span><span class="sxs-lookup"><span data-stu-id="649d4-121">Cancel, Cancel</span></span>|  
    |<span data-ttu-id="649d4-122">第一個文字方塊</span><span class="sxs-lookup"><span data-stu-id="649d4-122">First text box</span></span>|<span data-ttu-id="649d4-123">`Name`, `Text`</span><span class="sxs-lookup"><span data-stu-id="649d4-123">`Name`, `Text`</span></span>|<span data-ttu-id="649d4-124">SourceFile，""</span><span class="sxs-lookup"><span data-stu-id="649d4-124">SourceFile, ""</span></span>|  
    |<span data-ttu-id="649d4-125">第二個文字方塊</span><span class="sxs-lookup"><span data-stu-id="649d4-125">Second text box</span></span>|<span data-ttu-id="649d4-126">`Name`, `Text`</span><span class="sxs-lookup"><span data-stu-id="649d4-126">`Name`, `Text`</span></span>|<span data-ttu-id="649d4-127">CompareString，""</span><span class="sxs-lookup"><span data-stu-id="649d4-127">CompareString, ""</span></span>|  
    |<span data-ttu-id="649d4-128">第三個文字方塊</span><span class="sxs-lookup"><span data-stu-id="649d4-128">Third text box</span></span>|<span data-ttu-id="649d4-129">`Name`, `Text`</span><span class="sxs-lookup"><span data-stu-id="649d4-129">`Name`, `Text`</span></span>|<span data-ttu-id="649d4-130">WordsCounted，"0"</span><span class="sxs-lookup"><span data-stu-id="649d4-130">WordsCounted, "0"</span></span>|  
    |<span data-ttu-id="649d4-131">第四個文字方塊</span><span class="sxs-lookup"><span data-stu-id="649d4-131">Fourth text box</span></span>|<span data-ttu-id="649d4-132">`Name`, `Text`</span><span class="sxs-lookup"><span data-stu-id="649d4-132">`Name`, `Text`</span></span>|<span data-ttu-id="649d4-133">LinesCounted，"0"</span><span class="sxs-lookup"><span data-stu-id="649d4-133">LinesCounted, "0"</span></span>|  
  
4.  <span data-ttu-id="649d4-134">加入每個文字方塊旁邊的標籤。</span><span class="sxs-lookup"><span data-stu-id="649d4-134">Add a label next to each text box.</span></span> <span data-ttu-id="649d4-135">設定`Text`每一個標籤，如下表所示的屬性。</span><span class="sxs-lookup"><span data-stu-id="649d4-135">Set the `Text` property for each label as shown in the following table.</span></span>  
  
    |<span data-ttu-id="649d4-136">物件</span><span class="sxs-lookup"><span data-stu-id="649d4-136">Object</span></span>|<span data-ttu-id="649d4-137">屬性</span><span class="sxs-lookup"><span data-stu-id="649d4-137">Property</span></span>|<span data-ttu-id="649d4-138">設定</span><span class="sxs-lookup"><span data-stu-id="649d4-138">Setting</span></span>|  
    |------------|--------------|-------------|  
    |<span data-ttu-id="649d4-139">第一個標籤</span><span class="sxs-lookup"><span data-stu-id="649d4-139">First label</span></span>|`Text`|<span data-ttu-id="649d4-140">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="649d4-140">Source File</span></span>|  
    |<span data-ttu-id="649d4-141">第二個標籤</span><span class="sxs-lookup"><span data-stu-id="649d4-141">Second label</span></span>|`Text`|<span data-ttu-id="649d4-142">比較字串</span><span class="sxs-lookup"><span data-stu-id="649d4-142">Compare String</span></span>|  
    |<span data-ttu-id="649d4-143">第三個標籤</span><span class="sxs-lookup"><span data-stu-id="649d4-143">Third label</span></span>|`Text`|<span data-ttu-id="649d4-144">符合的文字</span><span class="sxs-lookup"><span data-stu-id="649d4-144">Matching Words</span></span>|  
    |<span data-ttu-id="649d4-145">第四個標籤</span><span class="sxs-lookup"><span data-stu-id="649d4-145">Fourth label</span></span>|`Text`|<span data-ttu-id="649d4-146">計算程式碼行</span><span class="sxs-lookup"><span data-stu-id="649d4-146">Lines Counted</span></span>|  
  
### <a name="to-create-a-backgroundworker-component-and-subscribe-to-its-events"></a><span data-ttu-id="649d4-147">若要建立 BackgroundWorker 元件，並訂閱其事件</span><span class="sxs-lookup"><span data-stu-id="649d4-147">To create a BackgroundWorker component and subscribe to its events</span></span>  
  
1.  <span data-ttu-id="649d4-148">新增<xref:System.ComponentModel.BackgroundWorker>元件從**元件**區段**工具箱**至表單。</xref:System.ComponentModel.BackgroundWorker></span><span class="sxs-lookup"><span data-stu-id="649d4-148">Add a <xref:System.ComponentModel.BackgroundWorker> component from the **Components** section of the **ToolBox** to the form.</span></span> <span data-ttu-id="649d4-149">它會顯示在表單的元件匣。</span><span class="sxs-lookup"><span data-stu-id="649d4-149">It will appear in the form's component tray.</span></span>  
  
2.  <span data-ttu-id="649d4-150">設定下列屬性 BackgroundWorker1 物件。</span><span class="sxs-lookup"><span data-stu-id="649d4-150">Set the following properties for the BackgroundWorker1 object.</span></span>  
  
    |<span data-ttu-id="649d4-151">屬性</span><span class="sxs-lookup"><span data-stu-id="649d4-151">Property</span></span>|<span data-ttu-id="649d4-152">設定</span><span class="sxs-lookup"><span data-stu-id="649d4-152">Setting</span></span>|  
    |--------------|-------------|  
    |`WorkerReportsProgress`|<span data-ttu-id="649d4-153">True</span><span class="sxs-lookup"><span data-stu-id="649d4-153">True</span></span>|  
    |`WorkerSupportsCancellation`|<span data-ttu-id="649d4-154">True</span><span class="sxs-lookup"><span data-stu-id="649d4-154">True</span></span>|  
  
### <a name="to-define-the-method-that-will-run-on-a-separate-thread"></a><span data-ttu-id="649d4-155">定義會在個別的執行緒執行的方法</span><span class="sxs-lookup"><span data-stu-id="649d4-155">To define the method that will run on a separate thread</span></span>  
  
1.  <span data-ttu-id="649d4-156">從**專案**] 功能表上，選擇 [**加入類別**將類別加入至專案。</span><span class="sxs-lookup"><span data-stu-id="649d4-156">From the **Project** menu, choose **Add Class** to add a class to the project.</span></span> <span data-ttu-id="649d4-157">**加入新項目**對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="649d4-157">The **Add New Item** dialog box is displayed.</span></span>  
  
2.  <span data-ttu-id="649d4-158">選取**類別**從 [範本] 視窗並輸入`Words.vb`[名稱] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="649d4-158">Select **Class** from the templates window and enter `Words.vb` in the name field.</span></span>  
  
3.  <span data-ttu-id="649d4-159">按一下 [加入] ****。</span><span class="sxs-lookup"><span data-stu-id="649d4-159">Click **Add**.</span></span> <span data-ttu-id="649d4-160">`Words`類別會顯示。</span><span class="sxs-lookup"><span data-stu-id="649d4-160">The `Words` class is displayed.</span></span>  
  
4.  <span data-ttu-id="649d4-161">將下列程式碼加入 `Words` 類別：</span><span class="sxs-lookup"><span data-stu-id="649d4-161">Add the following code to the `Words` class:</span></span>  
  
    ```vb  
    Public Class Words  
        ' Object to store the current state, for passing to the caller.  
        Public Class CurrentState  
            Public LinesCounted As Integer  
            Public WordsMatched As Integer  
        End Class  
  
        Public SourceFile As String  
        Public CompareString As String  
        Private WordCount As Integer = 0  
        Private LinesCounted As Integer = 0  
  
        Public Sub CountWords(  
            ByVal worker As System.ComponentModel.BackgroundWorker,  
            ByVal e As System.ComponentModel.DoWorkEventArgs  
        )  
            ' Initialize the variables.  
            Dim state As New CurrentState  
            Dim line = ""  
            Dim elapsedTime = 20  
            Dim lastReportDateTime = Now  
  
            If CompareString Is Nothing OrElse  
               CompareString = System.String.Empty Then  
  
               Throw New Exception("CompareString not specified.")  
            End If  
  
            Using myStream As New System.IO.StreamReader(SourceFile)  
  
                ' Process lines while there are lines remaining in the file.  
                Do While Not myStream.EndOfStream  
                    If worker.CancellationPending Then  
                        e.Cancel = True  
                        Exit Do  
                    Else  
                        line = myStream.ReadLine  
                        WordCount += CountInString(line, CompareString)  
                        LinesCounted += 1  
  
                        ' Raise an event so the form can monitor progress.  
                        If Now > lastReportDateTime.AddMilliseconds(elapsedTime) Then  
                            state.LinesCounted = LinesCounted  
                            state.WordsMatched = WordCount  
                            worker.ReportProgress(0, state)  
                            lastReportDateTime = Now  
                        End If  
  
                        ' Uncomment for testing.  
                        'System.Threading.Thread.Sleep(5)  
                    End If  
                Loop  
  
                ' Report the final count values.  
                state.LinesCounted = LinesCounted  
                state.WordsMatched = WordCount  
                worker.ReportProgress(0, state)  
            End Using  
        End Sub  
  
        Private Function CountInString(  
            ByVal SourceString As String,  
            ByVal CompareString As String  
        ) As Integer  
            ' This function counts the number of times  
            ' a word is found in a line.  
            If SourceString Is Nothing Then  
                Return 0  
            End If  
  
            Dim EscapedCompareString =  
                System.Text.RegularExpressions.Regex.Escape(CompareString)  
  
            ' To count all occurrences of the string, even within words, remove  
            ' both instances of "\b".  
            Dim regex As New System.Text.RegularExpressions.Regex(  
                "\b" + EscapedCompareString + "\b",  
                System.Text.RegularExpressions.RegexOptions.IgnoreCase)  
  
            Dim matches As System.Text.RegularExpressions.MatchCollection  
            matches = regex.Matches(SourceString)  
            Return matches.Count  
        End Function  
    End Class  
    ```  
  
### <a name="to-handle-events-from-the-thread"></a><span data-ttu-id="649d4-162">處理執行緒中的事件</span><span class="sxs-lookup"><span data-stu-id="649d4-162">To handle events from the thread</span></span>  
  
-   <span data-ttu-id="649d4-163">將下列事件處理常式加入至您的主要表單︰</span><span class="sxs-lookup"><span data-stu-id="649d4-163">Add the following event handlers to your main form:</span></span>  
  
    ```vb  
    Private Sub BackgroundWorker1_RunWorkerCompleted(   
        ByVal sender As Object,   
        ByVal e As System.ComponentModel.RunWorkerCompletedEventArgs  
      ) Handles BackgroundWorker1.RunWorkerCompleted  
  
        ' This event handler is called when the background thread finishes.  
        ' This method runs on the main thread.  
        If e.Error IsNot Nothing Then  
            MessageBox.Show("Error: " & e.Error.Message)  
        ElseIf e.Cancelled Then  
            MessageBox.Show("Word counting canceled.")  
        Else  
            MessageBox.Show("Finished counting words.")  
        End If  
    End Sub  
  
    Private Sub BackgroundWorker1_ProgressChanged(   
        ByVal sender As Object,   
        ByVal e As System.ComponentModel.ProgressChangedEventArgs  
      ) Handles BackgroundWorker1.ProgressChanged  
  
        ' This method runs on the main thread.  
        Dim state As Words.CurrentState =   
            CType(e.UserState, Words.CurrentState)  
        Me.LinesCounted.Text = state.LinesCounted.ToString  
        Me.WordsCounted.Text = state.WordsMatched.ToString  
    End Sub  
    ```  
  
### <a name="to-start-and-call-a-new-thread-that-runs-the-wordcount-method"></a><span data-ttu-id="649d4-164">若要開始，並呼叫新的執行緒可執行的 WordCount 方法</span><span class="sxs-lookup"><span data-stu-id="649d4-164">To start and call a new thread that runs the WordCount method</span></span>  
  
1.  <span data-ttu-id="649d4-165">將下列程序新增至您的程式︰</span><span class="sxs-lookup"><span data-stu-id="649d4-165">Add the following procedures to your program:</span></span>  
  
    ```vb  
    Private Sub BackgroundWorker1_DoWork(   
        ByVal sender As Object,   
        ByVal e As System.ComponentModel.DoWorkEventArgs  
      ) Handles BackgroundWorker1.DoWork  
  
        ' This event handler is where the actual work is done.  
        ' This method runs on the background thread.  
  
        ' Get the BackgroundWorker object that raised this event.  
        Dim worker As System.ComponentModel.BackgroundWorker  
        worker = CType(sender, System.ComponentModel.BackgroundWorker)  
  
        ' Get the Words object and call the main method.  
        Dim WC As Words = CType(e.Argument, Words)  
        WC.CountWords(worker, e)  
    End Sub  
  
    Sub StartThread()  
        ' This method runs on the main thread.  
        Me.WordsCounted.Text = "0"  
  
        ' Initialize the object that the background worker calls.  
        Dim WC As New Words  
        WC.CompareString = Me.CompareString.Text  
        WC.SourceFile = Me.SourceFile.Text  
  
        ' Start the asynchronous operation.  
        BackgroundWorker1.RunWorkerAsync(WC)  
    End Sub  
    ```  
  
2.  <span data-ttu-id="649d4-166">呼叫`StartThread`方法從`Start`表單上的按鈕︰</span><span class="sxs-lookup"><span data-stu-id="649d4-166">Call the `StartThread` method from the `Start` button on your form:</span></span>  
  
    ```vb  
    Private Sub Start_Click() Handles Start.Click  
        StartThread()  
    End Sub  
    ```  
  
### <a name="to-implement-a-cancel-button-that-stops-the-thread"></a><span data-ttu-id="649d4-167">若要實作 [取消] 按鈕，停止執行緒</span><span class="sxs-lookup"><span data-stu-id="649d4-167">To implement a Cancel button that stops the thread</span></span>  
  
-   <span data-ttu-id="649d4-168">呼叫`StopThread`程序從`Click`事件處理常式`Cancel` 按鈕。</span><span class="sxs-lookup"><span data-stu-id="649d4-168">Call the `StopThread` procedure from the `Click` event handler for the `Cancel` button.</span></span>  
  
    ```vb  
    Private Sub Cancel_Click() Handles Cancel.Click  
        ' Cancel the asynchronous operation.  
        Me.BackgroundWorker1.CancelAsync()  
    End Sub  
    ```  
  
## <a name="testing"></a><span data-ttu-id="649d4-169">測試</span><span class="sxs-lookup"><span data-stu-id="649d4-169">Testing</span></span>  
 <span data-ttu-id="649d4-170">您現在可以測試應用程式，確定它運作正常。</span><span class="sxs-lookup"><span data-stu-id="649d4-170">You can now test the application to make sure it works correctly.</span></span>  
  
#### <a name="to-test-the-application"></a><span data-ttu-id="649d4-171">若要測試應用程式</span><span class="sxs-lookup"><span data-stu-id="649d4-171">To test the application</span></span>  
  
1.  <span data-ttu-id="649d4-172">按 F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="649d4-172">Press F5 to run the application.</span></span>  
  
2.  <span data-ttu-id="649d4-173">顯示表單時，請輸入您想要在測試的檔案的檔案路徑`sourceFile`方塊。</span><span class="sxs-lookup"><span data-stu-id="649d4-173">When the form is displayed, enter the file path for the file you want to test in the `sourceFile` box.</span></span> <span data-ttu-id="649d4-174">例如，假設您的測試檔名為 Test.txt，輸入 C:\Test.txt。</span><span class="sxs-lookup"><span data-stu-id="649d4-174">For example, assuming your test file is named Test.txt, enter C:\Test.txt.</span></span>  
  
3.  <span data-ttu-id="649d4-175">在第二個文字方塊中，輸入單字或片語來搜尋文字檔案中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="649d4-175">In the second text box, enter a word or phrase for the application to search for in the text file.</span></span>  
  
4.  <span data-ttu-id="649d4-176">按一下 `Start` 按鈕。</span><span class="sxs-lookup"><span data-stu-id="649d4-176">Click the `Start` button.</span></span> <span data-ttu-id="649d4-177">`LinesCounted`按鈕應該開始立即遞增。</span><span class="sxs-lookup"><span data-stu-id="649d4-177">The `LinesCounted` button should begin incrementing immediately.</span></span> <span data-ttu-id="649d4-178">在完成時，應用程式就會顯示 「 完成計數 」 訊息。</span><span class="sxs-lookup"><span data-stu-id="649d4-178">The application displays the message "Finished Counting" when it is done.</span></span>  
  
#### <a name="to-test-the-cancel-button"></a><span data-ttu-id="649d4-179">若要測試的 [取消] 按鈕</span><span class="sxs-lookup"><span data-stu-id="649d4-179">To test the Cancel button</span></span>  
  
1.  <span data-ttu-id="649d4-180">按 F5 以啟動應用程式，並輸入檔案名稱，並搜尋文字中先前的程序所述。</span><span class="sxs-lookup"><span data-stu-id="649d4-180">Press F5 to start the application, and enter the file name and search word as described in the previous procedure.</span></span> <span data-ttu-id="649d4-181">請確定您選擇的檔案夠大，以確定您有時間完成之前取消此程序。</span><span class="sxs-lookup"><span data-stu-id="649d4-181">Make sure that the file you choose is large enough to ensure you will have time to cancel the procedure before it is finished.</span></span>  
  
2.  <span data-ttu-id="649d4-182">按一下 [ `Start` ] 按鈕以啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="649d4-182">Click the `Start` button to start the application.</span></span>  
  
3.  <span data-ttu-id="649d4-183">按一下 `Cancel` 按鈕。</span><span class="sxs-lookup"><span data-stu-id="649d4-183">Click the `Cancel` button.</span></span> <span data-ttu-id="649d4-184">應用程式應該立刻停止計數。</span><span class="sxs-lookup"><span data-stu-id="649d4-184">The application should stop counting immediately.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="649d4-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="649d4-185">Next Steps</span></span>  
 <span data-ttu-id="649d4-186">此應用程式包含一些基本錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="649d4-186">This application contains some basic error handling.</span></span> <span data-ttu-id="649d4-187">它會偵測空白的搜尋字串。</span><span class="sxs-lookup"><span data-stu-id="649d4-187">It detects blank search strings.</span></span> <span data-ttu-id="649d4-188">您可以讓程式更穩固處理其他錯誤，例如超過文字或程式行，就可以計算的最大數目。</span><span class="sxs-lookup"><span data-stu-id="649d4-188">You can make this program more robust by handling other errors, such as exceeding the maximum number of words or lines that can be counted.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="649d4-189">另請參閱</span><span class="sxs-lookup"><span data-stu-id="649d4-189">See Also</span></span>  
 <span data-ttu-id="649d4-190">[執行緒處理 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/index.md) </span><span class="sxs-lookup"><span data-stu-id="649d4-190">[Threading (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/index.md) </span></span>  
<span data-ttu-id="649d4-191"> [逐步解說︰ 撰寫簡單的多執行緒的元件，使用 Visual Basic](http://msdn.microsoft.com/library/05693b70-3566-4d91-9f2c-c9bc4ccb3001) </span><span class="sxs-lookup"><span data-stu-id="649d4-191"> [Walkthrough: Authoring a Simple Multithreaded Component with Visual Basic](http://msdn.microsoft.com/library/05693b70-3566-4d91-9f2c-c9bc4ccb3001) </span></span>  
<span data-ttu-id="649d4-192"> [如何：訂閱及取消訂閱事件](../../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)</span><span class="sxs-lookup"><span data-stu-id="649d4-192"> [How to: Subscribe to and Unsubscribe from Events](../../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)</span></span>