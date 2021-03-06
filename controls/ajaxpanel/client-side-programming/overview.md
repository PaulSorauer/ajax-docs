---
title: Overview
page_title: Client-side Programming Overview | RadAjax for ASP.NET AJAX Documentation
description: Overview
slug: ajaxpanel/client-side-programming/overview
tags: overview
published: True
position: 0
---

# Client-side Programming Overview



You can use the client-side API to execute your own JavaScript functions at certain stages of the AJAX request. Additionally, you can use a generic JavaScript function to make explicit AJAX requests to the server from the client. This help article discusses many of functions.

>note You can construct the JavaScript function calls manually or alternatively use the server-side method **GetAjaxEventReference** and have Telerik **RadAjax** generate the necessary code for you.
>


>note  **RadAjax** for ASP.NET AJAX requires enclosing the server code blocks inside a **RadCodeBlock** control. More information is available here:[RadCodeBlock and RadScriptBlock]({%slug ajaxmanager/radcodeblock-and-radscriptblock%}).
>


## ajaxRequest(arguments)

There are cases in which you may want to trigger postback/ajax request to the server. In this cases you can use the **ajaxRequest(arguments)** function to initiate a generic AJAX request. When using this function, the event target defaults to the **RadAjaxPanel** or **RadAjaxManager** instance. The **arguments** are the parameters that the control had used when it raised the request.

## AjaxRequest Event

When **ajaxRequest** function is called on the client it can be handled in the **AjaxRequest** event handler on the server, as shown in **Example 1**.

Example 1: Performe ajax request on the client and handle it on the server.

````JavaScript
	    <telerik:RadCodeBlock ID="RadCodeBlock1" runat="server">
	        <script type="text/javascript">
	
	            function InitiateAjaxRequest(arguments) {
	                var ajaxPanel = $find("<%= RadAjaxPanel1.ClientID %>");
	                ajaxPanel.ajaxRequest(arguments);
	            }
	        </script>
	    </telerik:RadCodeBlock>
````



````C#
	    private void RadAjaxPanel1_AjaxRequest(object sender, AjaxRequestEventArgs e)
	    {
	        //code to handle the generic AJAX request
	    }  
	
	
````
````VB.NET
	    Private Sub RadAjaxPanel1_AjaxRequest(ByVal sender As Object, ByVal e As AjaxRequestEventArgs)
	        'code to handle the generic AJAX request
	    End Sub
````



## ajaxRequestWithTarget(eventTarget, eventArgument)

You can call the **ajaxRequestWithTarget(eventTarget, eventArgument)** function to simulate a postback/AJAX request send by another control (besides **RadAjaxManager** or **RadAjaxPanel**) with the specified UniqueID and specifiedarguments. The function’s execution can be handled by the corresponding event (i.e., Button_Click) on the server.


| Parameters | Description |
| ------ | ------ |
| **eventTarget** |The control that should raise a postback event. You should always use the control's UniqueID..|
| **eventArgument** |This is an optional argument for the event.|

>note  **ajaxRequestWithTarget** is designed as a substitute of the standard **doPostBack function. Thus, you need to overridethe **RaisePostBackEvent** of the page in order to get its argument server-side.
>


**Example 2** shows how to use AjaxRequestWithTarget.

Example 3: The AjaxButton forces the Button to raise a postback event.

````ASPNET
		<asp:ScriptManager ID="ScriptManager" runat="server" />	    
	    
	    <telerik:RadAjaxPanel ID="RadAjaxPanel1" runat="server">
			<input type="button" onclick="AjaxRequestButton(); return false;" value="AjaxButton" />
			<asp:Button ID="Button1" runat="server" Text="Button" OnClick="Button1_Click"></asp:Button>
			<asp:TextBox ID="TextBox1" runat="server" Text=""></asp:TextBox>  
	    </telerik:RadAjaxPanel>
````



````JavaScript
	    <telerik:RadCodeBlock ID="cb1" runat="server">
	        <script type="text/javascript">
	            function AjaxRequestButton(arguments) {
	                var ajaxPanel = $find("<%= RadAjaxPanel1.ClientID %>");
	                ajaxPanel.ajaxRequestWithTarget('<%= Button1.UniqueID %>', '');
	            }
	        </script>
	    </telerik:RadCodeBlock>
````



And in the code-behind:



````C#
	    protected void Button1_Click(object sender, System.EventArgs e)
	    {
	        TextBox1.Text = DateTime.Now.ToLongTimeString();
	    }
````
````VB.NET
	    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs)
	        TextBox1.Text = DateTime.Now
	    End Sub
````


You can see the working example by following this link:

[https://demos.telerik.com/aspnet-ajax/Ajax/Examples/Manager/ClientSideAPI/DefaultCS.aspx](https://demos.telerik.com/aspnet-ajax/Ajax/Examples/Manager/ClientSideAPI/DefaultCS.aspx)

# See Also

 * [Overview]({%slug ajaxpanel/overview%})

 * [Demo: RadAjaxManager Client-side API](https://demos.telerik.com/aspnet-ajax/ajax/examples/manager/clientsideapi/defaultcs.aspx)
