---
title: About Windowless Rich Edit Controls
description: A windowless rich edit control, also known as a text services object, is an object that provides the functionality of a rich edit control without providing the window.
ms.assetid: '880a704d-776a-49d3-be31-0328af408e3b'
---

# About Windowless Rich Edit Controls

A windowless rich edit control, also known as a text services object, is an object that provides the functionality of a [rich edit control](rich-edit-controls.md) without providing the window. To provide the functionality of a window, such as the ability to receive messages and a device context into which it can draw, windowless rich edit controls use a pair of interfaces: [**ITextServices**](itextservices.md) and [**ITextHost**](itexthost.md).

To create a windowless rich edit control, call the [**CreateTextServices**](createtextservices.md) function with a pointer to your implementation of the [**ITextHost**](itexthost.md) interface. **CreateTextServices** returns an [**IUnknown**](https://msdn.microsoft.com/library/windows/desktop/ms680509) pointer that you can query to retrieve a pointer to the [**ITextServices**](itextservices.md) implementation of the windowless control.

Msftedit.dll exports an interface identifier (IID) called **IID\_ITextServices** that you can use to query the [**IUnknown**](https://msdn.microsoft.com/library/windows/desktop/ms680509) pointer for the [**ITextServices**](itextservices.md) interface. The following example shows how to retrieve **IID\_ITextServices** and use it to get the **ITextServices** interface.


```
    .
    .
    .
    HRESULT hr;
    IUnknown* pUnk = NULL;
    ITextServices* pTextServices =  NULL;
    
    // Create an instance of the application-defined object that implements the 
    // ITextHost interface.
    TextHost* pTextHost = new TextHost();
    if (pTextHost == NULL) 
        goto errorHandler;

    // Create an instance of the text services object.
    hr = CreateTextServices(NULL, pTextHost, &amp;pUnk);
    if (FAILED(hr))
        goto errorHandler;
        
    // Retrieve the IID_ITextServices interface identifier from 
    // Msftedit.dll. The hmodRichEdit parameter is a handle to the 
    // Msftedit.dll module retrieved by a previous call to the 
    // GetModuleHandle function.
    IID* pIID_ITS = (IID*) (VOID*) GetProcAddress(hmodRichEdit, 
        "IID_ITextServices");
               
    // Retrieve the ITextServices interface.    
    hr = pUnk->QueryInterface(*pIID_ITS, (void **)&amp;pTextServices);
    if (FAILED(hr))
        goto errorHandler;
     .
     . 
     .   
     
```



Msftedit.dll also exports an interface identifier (IID) called **IID\_ITextHost** that can be used in a similar manner to query for the [**ITextHost**](itexthost.md) interface.

The [**ITextHost**](itexthost.md) interface has methods that the windowless control calls to retrieve information about your window. For example, the text services object calls the [**TxGetDC**](itexthost-txgetdc.md) method to retrieve a device context into which it can draw. The windowless control calls the [**TxNotify**](itexthost-txnotify.md) method to send notifications, such as the rich edit notification messages, to the text host. The text services object calls other **ITextHost** methods to request the text host to perform other window-related services. For example, the [**TxInvalidateRect**](itexthost-txinvalidaterect.md) method requests the text host to add a rectangle to the window's update region.

A standard rich edit control has a window procedure that processes system messages and messages from your application. You can use the control's window handle to send it messages for performing text editing and other operations. But a windowless rich edit control has no window procedure to receive and process messages. Instead, it provides an [**ITextServices**](itextservices.md) interface. To send messages to a windowless rich edit control, call the [**TxSendMessage**](itextservices-txsendmessage.md) method. You can use this method to send any of the rich edit messages or to pass on other messages that affect the control, such as system messages for mouse or keyboard input.

You can also create the text services object as part of a [COM-aggregated object](https://msdn.microsoft.com/library/windows/desktop/ms686558). This makes it easy to aggregate the text services object with a windowless Component Object Model (COM) object.

 

 



