RoyopaPDFBundle
===============

FPDF and FPDI Bundle for Symfony2

[![Build Status](https://travis-ci.org/royopa/RoyopaPdfBundle.png?branch=master)](https://travis-ci.org/royopa/RoyopaPdfBundle)

## Installation

### Step 1: Download the bundle using Composer

    $ composer require "royopa/pdf-bundle": "dev-master as 1.0"

Or

Add RoyopaPdfBundle to composer.json.

    {
        "require": {
            "royopa/pdf-bundle": "dev-master as 1.0"
        }
    }

Install the bundle:

    $ composer.phar update royopa/pdf-bundle

Composer will install the bundle with the required dependencies.

### Step 2: Enable the bundle

In your AppKernel add the following:

```php
    // app/AppKernel.php

    public function registerBundles()
    {
        $bundles = array(
            // ...
            new Royopa\PdfBundle\RoyopaPdfBundle(),
        );
    }
```

## Usage

```php
    use Royopa\PdfBundle\lib\PDF;

    $pdf = new PDF();

    $pagecount = $pdf->setSourceFile('oldPdf.pdf);

    for($i = 1; $i <= $pagecount; $i++) {
        
        $tplIdx = $pdf->importPage($i);
        
        $s = $pdf->getTemplatesize($tplIdx);
        
        // This gets it the right dimensions
        $pdf->AddPage($s['h'] > $s['w'] ? 'P' : 'L', array($s['w'], $s['h']), true); 
        $pdf->useTemplate($tplIdx, 0, 0, 0, 0, true);
        
        $pdf->SetFont('Arial','',8);
        $pdf->SetTextColor(168,168,168);
        
        $pdf->SetY(20);
        $pdf->SetX(80);
        
        $pdf->Write(0, 'modify my pdf');
    }

    $pdf->Output('newPdf.pdf, 'D');
```
