# Reporting Server

## [Birt](http://www.eclipse.org/birt/)
Currently using Birt for generating reports and invoices for the child center.
### Setup
1. Download Birt report designer
1. Create report using designer.
    * Connect to database using jdbc connector
1. Built-in report generator - create PDF versions of report.

## [Jasper](http://community.jaspersoft.com/)
* Seems to have more moving parts.
* Comes with a server component.

## [Pentaho Reporting](https://community.hds.com/docs/DOC-1009856-pentaho-reporting)
* Has an open source server.

## Currently using Birt to generate invoices.
* All data in postgres DB
* Connect to postgres DB via jdbc
* One view and sql queries to populate the reports
* Seems to work okay now.

## Goals
1. Mobile view of reports. Web based mobile.
1. Generate reports on demand. Always most relevant data
1. Generate invoices that will be sent via email.
1. Enable reports for printing. Hardcopies are always nice.
1. Want to spend time desigining the report but only have to do it once. Easier with a graphic editor than trying to mangle XML, JSON, etc.
1. Want to chart.

## Issue with Eclipse (starting up report server)
* [Eclipse Wiki](https://wiki.eclipse.org/Eclipse.ini)
    * Fix issue to set explicit JVM for Eclipse.
## Generating PDFS
* [Dynamic Jasper](http://dynamicjasper.com/) - Make dynamic reports.
* [Dynamic Reports](http://dynamicreports.org/) - Dynamic reports based on Jasper
* [Jasper Reports Library](https://community.jaspersoft.com/project/jasperreports-library)
* [Apache PDFBox](https://pdfbox.apache.org/) - PDFBox - manipulate PDF docs.
* [iText](https://itextpdf.com) - Java PDF library - have book PDF
