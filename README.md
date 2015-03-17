RoyopaPDFBundle
===============

FPDF and FPDI Bundle for Symfony2

[![Build Status](https://travis-ci.org/royopa/RoyopaPdfBundle.png?branch=master)](https://travis-ci.org/royopa/RoyopaPdfBundle)
[![Latest Stable Version](https://poser.pugx.org/royopa/pdf-bundle/v/stable.svg)](https://packagist.org/packages/royopa/pdf-bundle) [![Total Downloads](https://poser.pugx.org/royopa/pdf-bundle/downloads.svg)](https://packagist.org/packages/royopa/pdf-bundle) [![Latest Unstable Version](https://poser.pugx.org/royopa/pdf-bundle/v/unstable.svg)](https://packagist.org/packages/royopa/pdf-bundle) [![License](https://poser.pugx.org/royopa/pdf-bundle/license.svg)](https://packagist.org/packages/royopa/pdf-bundle)

Installation
============

Step 1: Download the Bundle
---------------------------

Open a command console, enter your project directory and execute the
following command to download the latest stable version of this bundle:

```bash
$ composer require "royopa/pdf-bundle": "dev-master as 1.0"
```

This command requires you to have Composer installed globally, as explained
in the [installation chapter](https://getcomposer.org/doc/00-intro.md)
of the Composer documentation.

Step 2: Enable the Bundle
-------------------------

Then, enable the bundle by adding the following line in the `app/AppKernel.php`
file of your project:

```php
<?php
// app/AppKernel.php

// ...
class AppKernel extends Kernel
{
    public function registerBundles()
    {
        $bundles = array(
            // ...

            new Royopa\PdfBundle\RoyopaPdfBundle(),
        );

        // ...
    }

    // ...
}
```

Step 3: Use the Bundle
----------------------

```php
<?php
// app/AppKernel.php

use Royopa\PdfBundle\lib\PDF;

// ...
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
