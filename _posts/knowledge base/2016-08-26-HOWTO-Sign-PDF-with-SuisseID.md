---
layout: post
category: knowledge-base
title: HOWTO Sign PDF with SuisseID
date: 26 Aug 2016
tags: SuisseID
---

Today I had some troubles signing a PDF document with my [SuisseID](https://suisseid.ch) (Smart card version). I first tried to sign the PDF document by using Adobe Acrobat Reader DC. Unfortunately the Adobe Acrobat Reader DC started hanging during the saving process of the signed document. Nevertheless the document got saved but the signature was invalid.

After a few non successful retries I thought about opening the PDF with another PDF program and strumbled over the solution. Signing a PDF document can be easily done by using the [SwissSigner Software](https://postsuisseid.ch/de/support/application) that can be downloaded [here](https://postsuisseid.ch/de/support/application). I'll show you step by step how to sign a PDF with the SwissSigner software

1. Open the PDF document with the SwissSigner Software
  
  <a href="{{ site.url }}/assets/screenshots/sign-pdf-with-suisseid-1.png" target="_blank">
    <img src="{{ site.url }}/assets/screenshots/sign-pdf-with-suisseid-1.png" alt="Screenshot - Sign PDF with SuisseID" border="1">
  </a>

1. Go to `Signature` and select `Sign`

  <a href="{{ site.url }}/assets/screenshots/sign-pdf-with-suisseid-2.png" target="_blank">
    <img src="{{ site.url }}/assets/screenshots/sign-pdf-with-suisseid-2.png" alt="Screenshot - Sign PDF with SuisseID" border="1">
  </a>

1. Click at the place in the document you want to place your signature
1. Click `Sign` button

  <a href="{{ site.url }}/assets/screenshots/sign-pdf-with-suisseid-3.png" target="_blank">
    <img src="{{ site.url }}/assets/screenshots/sign-pdf-with-suisseid-3.png" alt="Screenshot - Sign PDF with SuisseID" border="1">
  </a>

1. Enter your SuisseID password
1. Select the location you want to save your signed PDF to

Now you’re done and you PDF document with a valid signature!
