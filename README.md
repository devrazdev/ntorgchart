### What is MyBoss? ###
**MyBoss** is a tool for automatic organizational chart creation in PowerPoint on PC or Mac. Technically, it's a VBA solution — [PowerPoint file] with macros and a custom tab.

[PowerPoint file]: <https://github.com/devrazdev/MyBoss/raw/master/MyBoss.pptm>

---

### How do these org charts look like? ###

The slide below was automatically created with **MyBoss** using [example input data].

![MyBoss-demo](https://github.com/devrazdev/MyBoss/raw/master/misc/demo.gif)

Extended [product demo] is available on Youtube. 

[sample data]: <https://github.com/devrazdev/MyBoss/raw/master/sample%20input.xlsx>
[product demo]: <https://www.youtube.com/watch?v=Do3c5ff7b1c>

### Why should I use it? ###
There is a [growing] interest in creating org charts, and the most [common] approach is creating them in PowerPoint manually, but, starting from ~50 people it becomes too time-consuming. Once you start [searching] for automation software, you discover [Microsoft Visio]. Indeed, Visio lets you visualize org structures of any size by uploading existing data and automatically arranging shapes, but it has 2 issues:

1. Visual appeal. Automatic chart looks clumsy, usually requires manual adjustments
2. Flexibility. Visio org charts can't be natively pasted/edited in PowerPoint, so you get locked on Visio

Org chart automation has already become a feature of many cloud applications (ex. [Google Sheets], [OrgChartNow], [Lucidchart]). None of them have good chart appeal and very few allow export to PowerPoint. **MyBoss** creates beautiful org charts out of the box, and it's native for Microsoft Office suite. 

[growing]: <https://trends.google.com/trends/explore?q=create%20org%20chart&date=all>
[common]: <https://www.youtube.com/results?search_query=create+org+chart>
[searching]: <https://support.office.com/en-us/article/create-an-org-chart-in-office-9419815f-0d7f-4d8b-8220-822036b1fe2b>

[Microsoft Visio]: <https://products.office.com/en-us/visio/flowchart-software>
[Google Sheets]: <https://www.bettercloud.com/monitor/the-academy/create-an-org-structure-chart-in-google-sheets/>
[OrgChartNow]: <https://www.orgchartpro.com/products/orgchart-now-2/>
[Lucidchart]: <https://www.lucidchart.com/pages/how-to-make-an-org-chart>

### What are the main features? ###
-Check for data loop
-Chart customisation
-....

### What are system requirements? ###
You need Microsoft PowerPoint 16.* and Microsoft Excel 16.*. **MyBoss** manually tested under:
- PC: Microsoft PowerPoint 2016 MSO (16.0.9126.2259) 32-bit + Microsoft Excel 2016 MSO (16.0.9126.2259) 32-bit
- Mac: Microsoft PowerPoint for Mac Version 16.15 (180709) + Microsoft Excel for Mac Version 16.15 (180709)

### How to run it? ###
Since **MyBoss** is just a PowerPoint file, there is no installation required. However:

1. Since it's written in VBA, PowerPoint may ask you to enable running VBA code, when you open the file (depending on your Trust Center settings). If "Security warning" comes up, just click "Enable content".
2. **MAC ONLY:** Due to the file access restrictions  ([reading Excel files from PowerPoint require AppleScript]), you will need to put *MyBoss-browse_files_on_mac.scpt* to ~/Library/Application Scripts/com.microsoft.Powerpoint/, before running the **MyBoss**. Do not change the name of script since it's hardcoded!

To perform a test run:
1. Open *MyBoss.pptm*
2. Go to "Org chart" tab
3. Click "Open"
4. Select *example input data.xlsx*
5. Select the spreadsheet you like
6. Click "Upload"
7. Once loaded, click "Create org chart" -> "Single slide org structure"
8. Wait until it finishes

[reading Excel files from PowerPoint require AppleScript]: <https://developer.microsoft.com/en-us/office/blogs/VBA-improvements-in-Office-2016/>

---

## Developers corner ##

### Are there any hidden dependencies? ###
The only third-party module used is Tim Hall's custom implementation of Dictionary class  to support Mac ([available on github]). Thanks, Tim.

[available on github]: <https://github.com/VBA-tools/VBA-Dictionary>

### Why did you choose to make a VBA solution? ###
There are 3 ways to build custom solutions for Office suite:
1. VBA solution
2. Visual Studio Tools for Office (VSTO) Add-in
3. JavaScript API Add-in

Their comparison is presented [here] and [there]. Basically, Office for Mac doesn't support VSTO Add-ins and JavaScript API for PowerPoint is yet (July'18) too limited.

[here]: <https://docs.microsoft.com/en-us/visualstudio/vsto/vba-and-office-solutions-in-visual-studio-compared>
[there]: <https://docs.microsoft.com/en-us/office/dev/add-ins/overview/office-add-ins#StartBuildingApps_TypesofApps>

### What is the right data format? ###
Take a look at *example input data.xlsx*. Basic rules:
1. Each spreadsheet represents a full org strructure. It must include all employees.
2. One employee — one line.
3. Minimum required data for every employee (not CEO) - 4 fields:
    - Employee Surname
    - Employee Name
    - Reports To Surname (manager's surname)
    - Reports To Name (manager's name)
4. Minimum required data for CEO - 2 fields:
    - Employee Surname
    - Employee Name
5. CEO must have these fields empty (because nobody is managing CEO):
    - Reports To Surname
    - Reports To Name
    - Dotted Line Manager Surname
    - Dotted Line Manager

See "data_minimum" tab in *example input data.xlsx*.

### How to customize MyBoss on my own? ###
The sad news is that VBA code is stored inside the *MyBoss.pptm* file in binary format. So, if you want to customize  **MyBoss**, you will have to use Office Visual Basic Editor.

1. To customize logic (VBA):
    - PC: type Alt+F11 or go to "Developer" tab -> Visual Basic;
    - Mac: go to Tools -> Macro -> Visual Basic Editor.
2. To customize UI tab (Ribbon XML):
[Reference guide on UI], [Mac Ribbon examples], [Win Ribbon examples]
    - PC: Suggest using utility [OfficeCustomUIEditorSetup] 
    - Mac: Suggest you find a PC. [However], if you change the extension of *MyBoss.pptm* from PPTM to ZIP and look inside the archive, you will find the Ribbon XML, which then you can edit...


[Reference guide on UI]: <https://msdn.microsoft.com/en-us/library/dd926139(v=office.12).aspx>
[Mac Ribbon examples]: <https://www.rondebruin.nl/mac/macfiles/MacRibbonExamples.dmg>
[Win Ribbon examples]: <https://www.rondebruin.nl/win/winfiles/RibbonExampleFiles.zip>
[OfficeCustomUIEditorSetup]: http://openxmldeveloper.org/blog/b/openxmldeveloper/archive/2006/05/26/customuieditor.aspx
[However]: <https://support.office.com/en-us/article/extract-files-or-objects-from-a-powerpoint-file-85511e6f-9e76-41ad-8424-eab8a5bbc517>

### Troubleshooting ###
1. Restart your computer and try again
2. If issue persists, shoot me an e-mail at devrazdev@gmail.com. I will try to help as soon as possible

## Farewell ##
I would be happy to hear any feedback about your use of **MyBoss**. Feel free to write me at devrazdev@gmail.com. Thank you.
