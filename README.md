# CSV Link for After Effects

# File
In [this](/CSV-Setup.aep) file you'll find a basic setup for text dynamically connected to specific CSV cells and a basic CSV lower third setup. I've also included a [sample CSV](/CSV.csv).

## Things to know about CSVs in After Effects
1. CSV (or _Comma-Separated Values_) is a simple file format to store data in rows and columns. You can import and export them from Microsoft Excel or similar programs. However, I like to work directly on the .csv file in a code editing software (such as [VS Code](https://code.visualstudio.com/)) or a text editor, because of a quirk in the file format:
While confusingly being called _Comma-Separated Values_, CSV files can have different delimiters (most commonly semicolons and tabs), and Microsoft Excel will usually output semicolon-seperated values even if specified differently. On the other hand, **After Effects will only accept actual comma-separated CSV files.** To fix that, either export from Excel and replace all semicolons with commas in VS Code or use a simple [online helper program](https://onlinetools.com/csv/change-csv-delimiter) to do the job for you. Also make sure to export CSVs in UTF-8 encoding to prevent special characters to break the text.
2. The first line in a CSV is always the header, which After Effects can't read. If you want the header to be readable, insert a blank first line.
3. The way we access the CSV file is using a direct `footage("CSV.csv")`call, which means it doesn't reference the Layer in the current comp. However, it's generally a good idea to **always drop a CSV file into all Comps you're using it in**. If you don't, _Collect Files_ or _Reduce Project_ using After Effect's Dependencies tools will get rid of the file, because those tools dont look for Expression references to files. And, since _Collect Files_ is what After Effects does when you send a project to Media Encoder, your CSV data will simply not show up there.
4. The bigger the CSV becomes, the more performance issues you're likely to run into. To mitigate that problem, use `posterizeTime(0);` in the beginning of Expressions referencing the file to make After Effects calculate it just once on the first Frame. This will make the entire Property static and will ignore Keyframes, so keep that in mind.



# Basic CSV Text Layer Link
This is the basic rig I like to use. The `sourceText` grabs the value from the CSV file using two _Slider Controls_ to act as line and column selectors. I like to link those up to the Layer Name, because you're likely to have lots of layers referencing different bits of the CSV and this is a great way to duplicate layers to create news lines of text. You can, of course, disable the Expression on the _Slider Controls_ to control them manually.
![Comp 1_1](https://github.com/user-attachments/assets/3eb7cce8-4e35-493f-8f38-d2e0141f3c25)

# CSV Table
![Table Autoposition](https://github.com/user-attachments/assets/6a8f4391-6562-4816-8cc8-07eb17871487)

# Lower Third
![__1](https://github.com/user-attachments/assets/f2f3a167-5dfd-46fe-8aaf-ac05667b1030)
