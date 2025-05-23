---
layout: default-layout
title: Read barcodes with small module size - Dynamsoft Barcode Reader SDK
description: This page describes how to read barcodes with small module size in Dynamsoft Barcode Reader SDK.
keywords: small barcode, small module size
needAutoGenerateSidebar: false
---

# How to Read Barcodes with Small Module Size

A module is the narrowest "bar" in a 1D barcode, or the smallest "box" in a 2D barcode. Keep in mind this "bar" or "box" can be either light or dark. The figure below illustrates the module size of 1D and 2D barcodes.

<div align="center">
   <p><img src="assets/read-barcodes-with-small-module-size/sample-barcode-with-small-module-size.png" alt="Module size of barcodes" width="50%" /></p>
   <p>Figure 1 – Module size of 1D and 2D barcodes</p>
</div>

In some scenarios, the barcode is very small relative to the entire image, and its module size is even smaller, making it difficult for the library to read the barcode. In this case, we can use the parameter `BarcodeScaleModes` in to enlarge the barcode symbol for easier processing.


## Particular Parameter Required

Dynamsoft Barcode Reader (DBR) provides a parameter [`BarcodeScaleModes`]({{ site.dcvb_parameters_reference }}barcode-reader-task-settings/barcode-scale-modes.html) that allows you to control the scale-up process when targets in the image are too small. 

## Example

Below is an example illustrating how to configure the parameter `BarcodeScaleModes`.

* Update parameter `BarcodeScaleModes` in your JSON template

    ```json
    {
        "CaptureVisionTemplates": [
            {
                "Name": "CV_0",
                "ImageROIProcessingNameArray": ["TA_0" ]
            }       
        ],
        "TargetROIDefOptions" : [
            {
                "Name": "TA_0",
                "TaskSettingNameArray": [ "BR_0" ]
            }
        ],
        "BarcodeReaderTaskSettingOptions": [
            {
                "Name" : "BR_0",
                "SectionArray": [
                    {
                        "Section": "ST_REGION_PREDETECTION",
                        "ImageParameterName": "IP_0"
                    },
                    {
                        "Section": "ST_BARCODE_LOCALIZATION",
                        "ImageParameterName": "IP_0"
                    },
                    {
                        "Section": "ST_BARCODE_DECODING",
                        "ImageParameterName": "IP_0",
                        "StageArray": [
                            {
                                "Stage": "SST_SCALE_BARCODE_IMAGE",
                                "BarcodeScaleModes": [
                                    {
                                        "Mode": "BSM_LINEAR_INTERPOLATION", 
                                        "ModuleSizeThreshold": 3,
                                        "TargetModuleSize": 8,
                                        "AcuteAngleWithXThreshold": 0
                                    },
                                ]
                            }
                        ]
                    }
                ]
            }
        ],
        "ImageParameterOptions": [
            {
                "Name": "IP_0"
            }
        ]
    }
    ```

* Apply the above settings following the article [Use Templates for Configuring Parameters]({{ site.features }}use-runtimesettings-or-templates.html#json-template).
