<!-- TITLE: Unzip Portal -->
<!-- SUBTITLE: For large Unzip files to be deployed in S2 -->

# Unzip 
You can reach it either by directl IP http://10.61.201.129:8080/ or by going to http://unzip.savvy.work/


**Input Bucket Folder examples**: "photos/", "photos", "photos/2018/" , "photos/2018" , "/photos" or "/photos/2018". ("photos" and "2018" are folder names not bucket names)

**Path to target folder examples**: "photos/", "photos", "photos/2018/" , "photos/2018" , "/photos" or "/photos/2018"

**Regular expression to match target files example**: ".+/DATA/.+\.zip" for all zip files in sub-folder name DATA

If regular expression is provided, it will be used to match files inside zip file, folder path and file extension will be ignored
If regular expression is not provided:
If both folder path and file extension are provided, they are used together
If both folder path and file extension are not provided, all files inside zip file will be extracted
If only folder path or file extension is provided, the one is provided will be used




    <h1>Wiki</h1>
    <hr>
    <h2>Unzip portal at a glance</h2>
    <p>
      Unzip portal (UP) is used to unzip large files which lambda cannot do. UP does not handle any transform part.
    </p>
    <hr>
    <h2>Input fields</h2>
    <hr>
    <h5 class="font-weight-bold">Input Bucket (required)</h5>
    <p>Name of S3 bucket that stores zip files need to be extracted.</p>

    <h5 class="font-weight-bold">Input Bucket Folder (optional)</h5>
    <p>If you want to unzip files inside one folder on S3 Bucket only, please enter the path to that folder in this field.</p>
    <p>For example: "photos", "photos/", "/photos", "/photos/", "photos/2018", "photos/2018/", "/photos/2018", "/photos/2018/"  </p>
    <p class="font-italic"><strong>Notes:</strong> "/" at beginning and ending are not important, you can ignore them or include them.</p>

    <h5 class="font-weight-bold">Output Bucket (required)</h5>
    <p>Name of S3 bucket that stores files after extracted.</p>

    <h5 class="font-weight-bold">Output Bucket Folder (optional)</h5>
    <p>If you want to store extracted files in a folder on S3 output bucket, please enter the path of that folder.</p>
    <p>For example: "photos", "photos/", "/photos", "/photos/", "photos/2018", "photos/2018/", "/photos/2018", "/photos/2018/"  </p>
    <p class="font-italic"><strong>Notes:</strong> "/" at beginning and ending are not important, you can ignore them or include them.</p>

    <h5 class="font-weight-bold">Path to target folder (optional)</h5>
    <p>
      One zip file may contain several different file types. You may only need to extract files in a particular folder.
      If that the case, please enter the path to that folder in this field.
    </p>
    <p>For examples:</p>
    <ul>
      <li>file "abc.zip" has two folders "data" and "docs". You want to extract files in "data" folder, then enter <strong>"data"</strong></li>
      <li>file "abc.zip" has two folders "data" and "docs", inside "data" folder there are "2012" and "2014" folders.
        You want to extract files in "2014" folder only, then enter <strong>"data/2014"</strong></li>
    </ul>

    <p>This field can be used together with "File extension" field or just only itself.</p>

    <p class="font-italic"><strong>Notes:</strong> "/" at beginning and ending are not important, you can ignore them or include them.</p>

    <h5 class="font-weight-bold">File extension (optional)</h5>
    <p>Extreact files that have a particular extension only such as ".csv", ".txt"</p>
    <p>This field can be used together with "Path to target folder" field or just only itself.</p>

    <h5 class="font-weight-bold">Regular expression to match target files (optional)</h5>
    <p>
      If regular expression is provided, it will be used to match files inside zip file, "Path to target folder"
      and "File extension" fields will be ignored.
    </p>
    <p>For example: ".+/DATA/.+\.zip" for all zip files in sub-folder name DATA</p>

  </div>