---
layout: post
category: knowledge-base
title: HOWTO Sign PDF with SuisseID
date: 26 Aug 2016
tags: SuisseID
---

Today I had some troubles signing a PDF document with my [SuisseID](http://suisseid.ch) (Smart card version). I first tried to sign the PDF document by using Adobe Acrobat Reader DC. Unfortunately the Adobe Acrobat Reader DC started hanging during the saving process of the signed document. Nevertheless the document got saved but the signature was invalid.

After a few non successful retries I thought about signing the PDF with another PDF program and strumbled over the solution. Signing a PDF document can be easily done by using the [Open eGov LocalSigner](https://www.openegov.admin.ch/egov/de/home/produkte/signieren/localsigner.html) that can be downloaded [here](http://www.e-service.admin.ch/wiki/display/openegovdoc/LocalSigner+Download). I'll show you step by step how to sign a PDF with the Open eGov LocalSigner application.

1. Plug your SuisseID into your computer
1. Open the `Open eGov LocalSigner`
1. Select (`Auswählen`) or drag and drop the PDF document you want to sign into the PDF preview area (Yellow area)
  
	<a href="{{ site.url }}/assets/screenshots/Open-eGov-LocalSigner-1.png" target="_blank">
	  <img src="{{ site.url }}/assets/screenshots/Open-eGov-LocalSigner-1.png" alt="Screenshot - Sign PDF with Open eGov LocalSigner" border="1">
	</a>

1. Click into the PDF preview area to select the position for the signature

	<a href="{{ site.url }}/assets/screenshots/Open-eGov-LocalSigner-2.png" target="_blank">
	  <img src="{{ site.url }}/assets/screenshots/Open-eGov-LocalSigner-2.png" alt="Screenshot - Sign PDF with Open eGov LocalSigner" border="1">
	</a>

1. Optionally adjust the name of the signed document

	<a href="{{ site.url }}/assets/screenshots/Open-eGov-LocalSigner-3.png" target="_blank">
	  <img src="{{ site.url }}/assets/screenshots/Open-eGov-LocalSigner-3.png" alt="Screenshot - Sign PDF with Open eGov LocalSigner" border="1">
	</a>

1. Click `Signieren` button

	<a href="{{ site.url }}/assets/screenshots/Open-eGov-LocalSigner-4.png" target="_blank">
	  <img src="{{ site.url }}/assets/screenshots/Open-eGov-LocalSigner-4.png" alt="Screenshot - Sign PDF with Open eGov LocalSigner" border="1">
	</a>

1. Enter your SuisseID password
1. Select the correct certificate and click again `Signieren`

	<a href="{{ site.url }}/assets/screenshots/Open-eGov-LocalSigner-5.png" target="_blank">
	  <img src="{{ site.url }}/assets/screenshots/Open-eGov-LocalSigner-5.png" alt="Screenshot - Sign PDF with Open eGov LocalSigner" border="1">
	</a>

1. Enter your SuisseID password

Now you’re done and you PDF document with a valid signature!

**IMPORTANT:** Close Fiddler during signing process as the time stamp service cannot be contacted successfully otherwise.
