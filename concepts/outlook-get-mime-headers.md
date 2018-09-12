# Get MIME content from a message (preview)

Multipurpose Internet Mail Extensions (MIME) is an industry email standard. Many email applications create messages in MIME format and save them in files with the .EML extension. 
Even though Outlook _does not save_ messages in MIME format, you can now use a `$value` segment to get the MIME content of an Outlook message. You can then save the content in a .EML file 
and attach the file to records in business systems, such as those for CRM, ERP, and bug tracking. 

> **Important:** This capability is currently available only in the /beta version. Similar to other API in preview status, it is subject to change. Do not use this capability in production apps. For more information, see [versioning and support](versioning_and_support.md).

## What is MIME?

MIME is a standard used by Internet email to transmit the following types of content via SMTP: 

- plain text message
- message with alternative content (i.e., in both plain text and HTML)
- reply message with the original message attached
- text message with attachments of image, audio, video, or application files  
- other message constructs.

## Get MIME content from an Outlook message

You can get the MIME representation of a message by appending the `$value` segment when 
[getting a message](../api-reference/beta/api/message_get.md):

<!-- { "blockType": "ignored" } -->
```http
GET /me/messages/{id}/$value
```

The following are typical MIME headers in a message. For more information, see [MIME](https://en.wikipedia.org/wiki/MIME).

- `MIME-Version` which indicates the message is MIME-formatted.
- `Content-Type` which indicates the media type of the message or a part of the message, represented by a *type* and *subtype*. It also 
includes a `boundary` field which specifies a string as the MIME boundary or as the encapsulation boundary, depending on the location of `Content-Type`. 
- `Content-Disposition` which provides details of an attachment such as its presentation style (`inline` or `attachment`), filenames, and 
creation and last modification dates.
- `Content-Transfer-Encoding` which specifies the encoding method to represent binary data.


## Example

The following is an example that requests a message to be returned with its MIME content.

<!-- { "blockType": "ignored" } -->
```http
GET /me/messages/4aade2547798441eab5188a7a2436bc1/$value
```

The following is the response. The MIME content begins with the `MIME-Version` header. 

<!-- { "blockType": "ignored" } -->
```http
Received: from contoso.com (10.194.241.197) by 
contoso.com (10.194.241.197) with Microsoft 
SMTP Server (version=TLS1_2, 
cipher=TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256) id 15.1.1374.0 via Mailbox 
Transport; Mon, 4 Sep 2017 03:00:08 -0700 
Received: from contoso.com (10.194.241.197) by 
contoso.com (10.194.241.197) with Microsoft 
SMTP Server (version=TLS1_2, 
cipher=TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256) id 15.1.1374.0; Mon, 4 Sep 
2017 03:00:07 -0700 
Received: from contoso.com 
([fe80::5bf:5059:4ca0:5017]) by contoso.com 
([fe80::5bf:5059:4ca0:5017%12]) with mapi id 15.01.1374.000; Mon, 4 Sep 2017 
03:00:01 -0700 
From: Administrator <admin@contoso.com> 
To: Administrator <admin@contoso.com> 
Subject: This email has attachment. 
Thread-Topic: This email has attachment. 
Thread-Index: AQHTJWSHSywMzSz8o0OJud48nG50GQ== 
Date: Mon, 4 Sep 2017 10:00:00 +0000 
Message-ID: 
                <4aade2547798441eab5188a7a2436bc1@contoso.com> 
Accept-Language: en-US 
Content-Language: en-US 
X-MS-Exchange-Organization-AuthAs: Internal 
X-MS-Exchange-Organization-AuthMechanism: 04 
X-MS-Exchange-Organization-AuthSource: 
                contoso.com 
X-MS-Has-Attach: yes 
X-MS-Exchange-Organization-Network-Message-Id: 
                0ffdb402-ec03-42c8-5d32-08d4f37bb517 
X-MS-Exchange-Organization-SCL: -1 
X-MS-TNEF-Correlator: 
X-MS-Exchange-Organization-RecordReviewCfmType: 0 
x-ms-publictraffictype: Emai

```http
MIME-Version: 1.0 
Content-Type: multipart/mixed; 
                boundary="_004_4aade2547798441eab5188a7a2436bc1contoso_" 
 
--_004_4aade2547798441eab5188a7a2436bc1contoso_ 
Content-Type: multipart/alternative; 
                boundary="_000_4aade2547798441eab5188a7a2436bc1contoso_" 
 
--_000_4aade2547798441eab5188a7a2436bc1contoso_ 
Content-Type: text/plain; charset="iso-8859-1" 
Content-Transfer-Encoding: quoted-printable 
 
The attachment is an email. 
 
--_000_4aade2547798441eab5188a7a2436bc1contoso_ 
Content-Type: text/html; charset="iso-8859-1" 
Content-Transfer-Encoding: quoted-printable 
 
<html> 
<head> 
<meta http-equiv=3D"Content-Type" content=3D"text/html; charset=3Diso-8859-= 
1"> 
<style type=3D"text/css" style=3D"display:none;"><!-- P {margin-top:0;margi= 
n-bottom:0;} --></style> 
</head> 
<body dir=3D"ltr"> 
<div id=3D"divtagdefaultwrapper" style=3D"font-size:12pt;color:#000000;font= 
-family:Calibri,Helvetica,sans-serif;" dir=3D"ltr"> 
<p>The attachment is an email.</p> 
</div> 
</body> 
</html> 
 
--_000_4aade2547798441eab5188a7a2436bc1contoso_-- 
 
--_004_4aade2547798441eab5188a7a2436bc1contoso_ 
Content-Type: application/octet-stream; name="Attachment email.eml" 
Content-Description: Attachment email.eml 
Content-Disposition: attachment; filename="Attachment email.eml"; size=408; 
                creation-date="Mon, 04 Sep 2017 09:59:43 GMT"; 
                modification-date="Mon, 04 Sep 2017 09:59:43 GMT" 
Content-Transfer-Encoding: base64 
 
RnJvbToJQWRtaW5pc3RyYXRvciA8YWRtaW5AdGVuYW50LUVYSEItMTQ3MS5jb20+DQpTZW50OglN 
b25kYXksIFNlcHRlbWJlciA0LCAyMDE3IDM6MjYgUE0NClRvOglTcml2YXJkaGFuIEhlYmJhcg0K 
U3ViamVjdDoJQXR0YWNobWVudCBlbWFpbA0KDQpJIHdpbGwgYXR0YWNoIHRoaXMgZW1haWwgdG8g 
YW5vdGhlciBtYWlsLg0K 
 
--_004_4aade2547798441eab5188a7a2436bc1contoso_-- 
```



