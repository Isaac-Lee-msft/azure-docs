---
title: What's new in Form Recognizer?
titleSuffix: Azure Cognitive Services
description: Understand the latest changes to the Form Recognizer API.
author: PatrickFarley
manager: nitinme

ms.service: cognitive-services
ms.subservice: forms-recognizer
ms.topic: conceptual
ms.date: 03/20/2020
ms.author: pafarley

---

# What's new in Form Recognizer?

The Form Recognizer service is updated on an ongoing basis. Use this article to stay up to date with feature enhancements, fixes, and documentation updates.

> [!NOTE]
> The quickstarts and guides for Form Recognizer always use the latest version of the API, unless specified.

## March 2020 

### Extraction Enhancements and bug fixes

This release includes extraction enhancements and accuracy improvements, specifically, the capability to label and extract multiple key/value pairs in the same line of text. In addition, we've fixed several bugs, including a fix that allows users to submit a file URL as the source to the [`analyzeForm`](https://westus2.dev.cognitive.microsoft.com/docs/services/form-recognizer-api-v2-preview/operations/AnalyzeWithCustomForm) and [`analyzeLayout`](https://westus2.dev.cognitive.microsoft.com/docs/services/form-recognizer-api-v2-preview/operations/AnalyzeLayoutAsync) APIs. 


**Enhancements**

* Added additional logs and telemetry for storage manager, time-to-results, and document complexity 
* Improved model performance
* Integrated latest pdfminer release
* Integrated new read layout OCR engine

**Bug fixes**

* Bug fix: Public version is no longer hard coded into the route
* Bug fix: Slow blob listings no longer block training 
* Bug fix: Kestrel unable to process malformed JSON for Analyze requests
* Bug fix: Get/Delete APIs return errors for non-existent models
* Bug fix: Isolate currency characters not detected
* Bug fix: Prediction takes longer than 60 seconds
* Bug fix: Unable to extract key/value pairs. List index out of range. 
 
### Form Recognizer Sample Labeling Tool is now open-source

The Form Recognizer Sample Labeling Tool is now available as an open-source project. You can integrate it within your solutions and make customer-specific changes to meet your needs.

For more information about the Form Recognizer Sample Labeling Tool, review the documentation available on [GitHub](https://github.com/microsoft/OCR-Form-Tools/blob/master/README.md).

### Labeling value types

Value types are now available for use with the Form Recognizer Sample Labeling Tool. These value types are currently supported: 

* String
* Number 
* Integer
* Date 
* Time

This image shows what value type selection looks like within the Form Recognizer Sample Labeling Tool:

> [!div class="mx-imgBorder"]
> ![Value type selection with sample labeling tool](./media/whats-new/formre-value-type.png)

The extracted table are available in the JSON output in `pageResults`.

### Table visualization 

The Form Recognizer Labeling Tool now displays tables that were recognized in the document. This lets you view the tables that have been recognized and extracted from the document, prior to labeling and analyzing with the Form Recognizer Sample Labeling Tool. This feature can be toggled on/off using the layers option. 

This is an example of how tables are recognized and extracted:

> [!div class="mx-imgBorder"]
> ![Table visualization using the sample labeling tool](./media/whats-new/formre-table-viz.png)

> [!IMPORTANT]
> Labeling tables isn't supported. If tables are not recognized and extrated automatically, you can only label them as key/value pairs. When labeling tables as key/value pairs, please label each cell as a value.

## January 2020

This release introduces the Form Recognizer 2.0 (preview). In the sections below, you'll find more information about new features, enhancements, and changes. 

### New features

* **Custom model**
  * **Train with labels** You can now train a custom model with manually labeled data. This results in better-performing models and can produce models that work with complex forms or forms containing values without keys.
  * **Asynchronous API** You can use async API calls to train with and analyze large data sets and files.
  * **TIFF file support** You can now train with and extract data from TIFF documents.
  * **Extraction accuracy improvements**

* **Prebuilt receipt model**
  * **Tip amounts** You can now extract tip amounts and other handwritten values.
  * **Line item extraction** You can extract line item values from receipts.
  * **Confidence values** You can view the model's confidence for each extracted value.
  * **Extraction accuracy improvements**

* **Layout extraction** You can now use the Layout API to extract text data and table data from your forms.

### Custom model API changes

All of the APIs for training and using custom models have been renamed, and some synchronous methods are now asynchronous. The following are major changes:

* The process of training a model is now asynchronous. You initiate training through the **/custom/models** API call. This call returns an operation ID, which you can pass into **custom/models/{modelID}** to return the training results.
* Key/value extraction is now initiated by the **/custom/models/{modelID}/analyze** API call. This call returns an operation ID, which you can pass into **custom/models/{modelID}/analyzeResults/{resultID}** to return the extraction results.
* Operation IDs for the Train operation are now found in the **Location** header of HTTP responses, not the **Operation-Location** header.

### Receipt API changes

The APIs for reading sales receipts have been renamed.

* Receipt data extraction is now initiated by the **/prebuilt/receipt/analyze** API call. This call returns an operation ID, which you can pass into **/prebuilt/receipt/analyzeResults/{resultID}** to return the extraction results.

### Output format changes

The JSON responses for all API calls have new formats. Some keys and values have been added, removed, or renamed. See the quickstarts for examples of the current JSON formats.

## Next steps

Complete a [quickstart](quickstarts/curl-train-extract.md) to get started with the [Form Recognizer APIs](https://westus2.dev.cognitive.microsoft.com/docs/services/form-recognizer-api-v2-preview/operations/AnalyzeWithCustomForm).