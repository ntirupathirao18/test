# Assignment

Packages:
 1. **PyPDF2**
 2. **difflib**
 
**Phase -1:**

Part - 1: The [url](https://www.sec.gov/foia/iareports/inva-archive.htm) has a list of zip files that are downloadable href links on them. The urls are extracted by use of bs4 package and a class BeautifulSoup. The soup extracts all href links which matches with the regular expression 'files/data/' and extract all links. The href links extracted with their contents, the contents are used for filtering from exempt and non- exempt. 

  The exempt links starts with exempt in their content name. The string *'/ia'* is searched in the href content name, the found index is added with a number 3 and 9 because this return a string with a date in it. The return date has first two digits of month and last two digits are year ending and finally the remaining digits are date, is pushed into list. All the extracted contents are pushed into dictionary by making the list into pandas series. A data frame is created passing a dict to it **sec_df**. 

 **Part - 2:** The zip files have to be downloaded from the given periods and the recent part is considered to be recent date in the zip upload part, it can be derived from by the use of max function on date column which gives a date and its url is being extracted from the data frame and downloading the zip file. 
  
  In other side, from the periods list, the each date is converted into year and month format on the date column is stored in the **per** variable. the periods list of dates are being searched in the **per** series variable. The found date has a url related to it, the url which downloads a zip file. The zip file is being opened and the contents is being considered there is only one file in it, the content file name is stored in **filename**, the **filename** is spilt into two parts to get the extension of file name. The extension **file name** is searched for txt,csv and xls file. The extension files are being load into the data frame **df_sec_i** which is append to list **df_get_Period** and opened zip file,contents is closed.  

**Phase - 2:** The [url](https://doppler.finra.org/doppler-lookup/api/v1/search/firms?hl=true&nrows=99000&query=Blackstone&r=2500&wt=json) contains a json file. The results are extracted from the json file and stored in the **d**. The **d** is a list with a dict, the results are filtered for the with *score > 0.4*  and searched for if *'bc_ia_scope'* field is active or not . The filtered fields are being searched over the address *345 PARK AVENUE'*  the results are being appened into a list **data_string['results']**, **data_string** is a dict. 
The **data_string** is converted into a json file and returned to the function. 

**Phase-3:** The json file again converted into **df** data frame with series are **bc_firm_name**  and **bc_source_id** . The **bc_source_id** is append to a [url]('https://adviserinfo.sec.gov/IAPD/IAPDFirmSummary.aspx?ORG_PK=), the url contains a pdf file under *part-2* link. The href links with regular expression *IAPD/Content/Common* is being searched and stored into the **urls** list.   

The **urls** contains pdf file which is parsed by the use of *PyPDF2* package with a class of pdfFileReader and the extrated text is stored in the **contents** and appened to list **contents_all** which consists of all the contents of pdf files. The *getDocumentInfo()* returns pdf information on document like *Author*,*date*,'Title*. The pdf information is being stored in the **information** list. The **Author** list is extracted from the **information** list, it is converted into pandas series and append to the data frame **df**. 

Now, the **check** consists of word where it has to be compared for the similarity ratio with the series of **Author** and stored in the **df** with series of **CloseRatio**.

