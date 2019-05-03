### Introduction

Printer service is a service which provides a simplified api for printer related operations. It processes requests from users, manipulates data into a format which can be used by printer MCU.  It is written using C++ and it uses Linux File Socket, Binder, Broadcast/Subscribe (Limited to Status Change Event) IPC methods.

### General Structure

Here is a diagram of general structure of the printer service:

<div class="mxgraph" style="max-width:100%;border:1px solid transparent;" data-mxgraph="{&quot;highlight&quot;:&quot;#0000ff&quot;,&quot;nav&quot;:true,&quot;resize&quot;:true,&quot;toolbar&quot;:&quot;zoom layers lightbox&quot;,&quot;edit&quot;:&quot;_blank&quot;,&quot;xml&quot;:&quot;&lt;mxfile modified=\&quot;2019-04-18T11:33:49.886Z\&quot; host=\&quot;www.draw.io\&quot; agent=\&quot;Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:66.0) Gecko/20100101 Firefox/66.0\&quot; etag=\&quot;rYMBUYI4mT7k869rG_4s\&quot; version=\&quot;10.6.3\&quot; type=\&quot;device\&quot;&gt;&lt;diagram id=\&quot;dQrV2Z9j8ETe149ZBXxr\&quot; name=\&quot;Page-1\&quot;&gt;3Vvfc9soEP5r/JiMEPr5GCdNOzfpNDO5zF2fbrCEbVpZqAgn9v31BxKSJZBtxZXs5JwHw4IQ/r7dZRfIBN6uNp8ZypZfaYyTiW3Fmwm8m9g2gKEjvqRkW0p8JywFC0Zi1WkneCL/YiW0lHRNYpy3OnJKE06ytjCiaYoj3pIhxuhru9ucJu23ZmiBDcFThBJT+heJ+bKUBq61k3/BZLGs3gws1bJCVWclyJcopq8NEfw0gbeMUl6WVptbnEjwKlzK5+73tNYTYzjlfR74+zF5WYLP7I8vPrqaP8zx6y94BdXkXlCyVr9YzZZvKwgYXacxlqNYEzh9XRKOnzIUydZXQbqQLfkqETUginOacsUiCERdDY8Zx5u9Ewc1HEKPMF1hzraii3rAB2pO2wpjNcTrjhBg+aVs2SDDVc8hpQOLeugdTKKgkHoDauAtoIEeoJEkuaUJZcWzcO7KPyHPOaM/caPFKz4K5oa8/AwDN4BeC+7QNtB2Lc9EG/ruSHDbHXB7CVcwtHD3fq1p1XCVF3p4IzqAINsU6FTtorSQ34+MpByzJ8xeiCBHDStmWY5cdjLIFeDyNoNtplKaYo1WJUIJWaSiGmH5WiGQVBHhbm5Uw4rEsXxNp8q0LXEEU4O+ZmqWaWqOZXJf+bjBqXeOW5rwq5ksklXhypus6OBymjWkD2iGk0eaE06obJ1RzulKdEhkwxRFPxcF4E3LLD6iS/GymzwrlxzJBqoqc7KRFE3VfO6WnMu16kYCYd9HcQqviVit5kRQya4j8Ub7PkYciS8pz2UnusrWQj+uXAH/fbGk1LJ/gHMF7OA6SxeD+Fa/RbgNu3yrYzJeCwen3DUoV0YqhF9vn9+pMQ7Bha1xYQUGF0HQ4XjHMj7gGmDjWERHqkoZX9IFTVHyaSfVYNn1eaDS+Ap+fmDOt8pzoTWnbfbwhvC/1eOy/F2Wr11Vu9s0mu62B12hnOxhLsRvo2sW4QMgeN2cMZwgTl7a43cxoB59pKRYqiqu22ssCDQOOWILzNVDGo31LE5n1jNs7Ikjvha+xxIEojhCOSfSwVh/LhlG8bDhzRx7UdQV3sR+OLOsQ4ZomGwu3ipm+oDnkle4k0yVN78bKizytKWxSgGantLuWBu9sczTN0icFmuKkD2QnONUFs/L2wg4227HinRWnAPTWGj0E/P/F87w4jiHHbFeGY/H5EW+UNn+LopPpNUbMf3XtUTF9tBK4pzO8qxsPFK3qrfN2C7wr/OBYgr70gFGULrYGyg0mB6AN+iAtn04ph/ygElbMFoy3LWF0OCtBG1K+EqgIdaXtdBv1hPZKrbPGI1wnh8HeFZH7d/WPCEp7jax2MVB7HSZWGDPYJFhD0CV47Wpgr7fz8TggXji97gydy6K4FqIvuAkG9iRnQllVwubgWeiDDtQBuMFzuaOxX25U/HMSfIRMT41+HFGg7jHzgBO4xu5BSzjxQTlOSkXVcS4KT6whSkwYts6I5GVRkoiq7ucpKhVScmkdxJSRvvHQj2TndaWnAl+JRs2V7H1XKVMoYxcxRgHBO2BnPC8SQ8ws56PqjLvRBVgIH/Sacqgh58B0IcaWx3MuP7c6uAf04d6L+Q6DO3WfogH/IM7IrLyiBkRKMk8+Y0O6eiuSNDTcYWX1Favra2uvhj11lVwmuMSOoK2jW6Z7JDvny+0dfMKDs7L6G+1TgBFoZzBsGbTlaaNZDZK+8Gk/07g+Iv1UdvwP4JtGMbhn2gcUDMOVz8LGtmNV+r3wfTRPqNCeh9BIaHV1qOT9dHVwtXz+OpqB7+vr672aEb11Ta8eIjTN8J5i00NaBphT9MAFw27HUtPwbQhxo5kBlPIM2btdejsNlXrXIpV7Yq+d83S7lbZ4Yma5Xj+4YHG1qxLJPc77/a9cmG9krnLaGTfzaZSJS4WBzhtF+VZpwYCoRaYumf2deb57JuvrdnZxjzfen6a9r2odsHAN9FuV7FSU/bevirvZlVnfMXJnnkPoL6idQm7cC5pFq6eZukrd1+zcI/tioxtFl3bbieYRddtTv1Qt7q80s9YTr7nbJvHMj3O8DVVf6u91Fdi9t6VUTj/3pU0p6Us9RlP63qgqfTA2q/fv3cVeP8lgcG15zaT59XfZj/kvc6TdKi/vvQ4xjtZQY741FH1xbEvqy/VSXrnbdLnHLPcoPB93Cdt6IvtFK0cKWKvQtlBXXOT7cNwdwX8sB3CQ5M8x3VN9vSlqAd7orr7z5dyadn9/xD89B8=&lt;/diagram&gt;&lt;/mxfile&gt;&quot;}"></div> 
 <script type="text/javascript" src="https://www.draw.io/js/viewer.min.js"></script>
 
 **Status Broadcasting Thread**: This thread is defined and run in PrinterService.cpp. It creates a [Android Broadcast](https://developer.android.com/guide/components/broadcasts) which notifies subscribers when printer status changes. See example usage in [example Java project](https://35.205.196.69/Project400TR/PrinterServiceTest).
  
 **Binder Listener**: This thread listens requests via binder IPC. See: [Android Binder](https://developer.android.com/reference/android/os/Binder), [Usage from a Java Application](http://10.134.120.26:8082/tokendoc/pos-projects/400tr/sw/printer-service/printer-driver-usage).
 
 **Socket Listener**: This thread listens requests Unix Socket IPC. See: [Example NDK Project](https://35.205.196.69/Project400TR/NDK_PrinterServiceClientExample)
 
 **Mutex**: Requests made via socket listener, via binder listener and periodic status checks by broadcasting thread are handled in an atomic way. That is, once a thread accesses the printer, operation cannot be interrupted by other threads.
 
 **Print Helper**: This class handles communication with printer MCU via USB. It processes requests into a format that is meaningfull for printer MCU, and prepares responses from MCU to be send back to user. For example, when a string is send by a user to be printed, printHelper converts string into a bitmap in accordance with selected font size and font face with the help of fontUtil and bitmapBuffer classes. Then it sends each line of produced bitmap to MCU with a print command.
 
 **Bitmap Buffer**: This class is used to hold proccessed binary data which will be send to printer line by line. In other words, it is used to encapsulate bitmap related functionality. Print helper uses one BitmapBuffer object to process one line of text at a time. To move on to a new line, it calls clean function of Bitmap buffer and reuses this object. That is, only one BitmapBuffer object is used to print multiple line of text. This is to avoid overuse of memory in case of a huge text input.  
 Note: In case a of printing a bmp file, a seperate Bitmapbuffer object is created for it.
 
 
 **Font Util**: To be defined
 
 
  **Printer MCU**: to be defined  
 
