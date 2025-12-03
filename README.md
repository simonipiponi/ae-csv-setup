# CSV Link for After Effects

## Download
> [!NOTE]
> In this [After Effects file](/CSV-Setup.aep) you'll find a couple of different setups. They're all described below. 
> I've also included a [sample CSV](/CSV.csv).

## Things to know about CSVs in After Effects

### 1. "Comma-Seperated Values" is a lie
CSV (or _Comma-Separated Values_) is a simple file format to store data in rows and columns. You can import and export them from _Microsoft Excel_ or similar programs. However, I like to work directly on the .csv file in a code editing software _(such as [VS Code](https://code.visualstudio.com/))_ or a text editor, because of a quirk in the file format:
While confusingly being called _Comma-Separated Values_, CSV files can have different delimiters (most commonly semicolons and tabs), and Microsoft Excel will usually output semicolon-seperated values even if specified differently. On the other hand, **After Effects will only accept actual comma-separated CSV files.** To fix that, either export from Excel and replace all semicolons with commas in VS Code or use a simple [online helper program](https://onlinetools.com/csv/change-csv-delimiter) to do the job for you. Or work directly in the CSV file and skip all that jazz.

This is the structure we're looking for:
```
Name, Profession, Age
Lucius Telljoy, Disgraced Magician, 43
Olialy Polly, Chilean singer-songwriter, 35
```

### 2. Special Characters work, but only if you're careful.
Make sure to export CSVs in UTF-8 encoding to prevent special characters `(ä,ü,ø,ß, ...)` from breaking the text. This isn't always the default setting, and depending on your program of choice, you might have to specify while "Saving As".

### 3. The first line isn't readable.
The first line in a CSV is always the header, which After Effects can't read.
If you want the header to be readable, insert a blank first line.

### 4. The file doesn't have to be in a composition. But it should be.
The way we access the CSV file is using a direct `footage("CSV.csv")` call, which means it doesn't reference the layer in the current composition. However, it's generally a good idea to **always drop a CSV file into all comps you're using it in**. If you don't, _Collect Files_ or _Reduce Project_ using After Effect's Dependencies tools will get rid of the file, because those tools don't look for Expression references to files. And, since _Collect Files_ is what After Effects does when you send a project to Media Encoder, your CSV data will simply not show up there.

### 5. Watch out for performance issues.
The bigger the CSV file and the more often it's referenced, the more performance issues you're likely to run into. To mitigate that problem, use `posterizeTime(0);` in the beginning of Expressions referencing the file to make After Effects calculate it just once on the first frame. This will make the entire property static and will ignore keyframes, so only use when you don't want to animate that property. I like to have the _Render Time_ visible in the timeline to see what's eating performance. 
> [!TIP]
> Layers with `Opacity: 0` are not rendered and thus don't impact Render Time. That's why I like to have the more complicated expressions on Null Objects (usually called _CTRL_), because Nulls by default have their opacity set to 0.



# Basic CSV Text Layer Link
This is the basic rig I like to use. The `sourceText` grabs the value from the CSV file using two _Slider Controls_ to act as line and column selectors. I like to link those up to the layer name, because you're likely to have lots of layers referencing different bits of the CSV and this is a great way to duplicate layers to create news lines of text. You can, of course, disable the Expression on the _Slider Controls_ to control them manually.

![comp 1_1](https://github.com/user-attachments/assets/3eb7cce8-4e35-493f-8f38-d2e0141f3c25)

# CSV Table
These are some of those CSV Text layer Rigs in action, paired with dynamic placing in rows and columns. The layer name controls the placing of the Text layers, and there's basic styling Pseudo Effects available to control cell sizes and paddings.

![Table Autoposition](https://github.com/user-attachments/assets/6a8f4391-6562-4816-8cc8-07eb17871487)

# Lower Third
Here the line and column Pseudo Effects were linked up the the comp name—while having static columns (e.g. Title/Subtitle), duplicating the comp (thus incrementing the suffix by one) will select the next line, updating the text accordingly. Great to set up line 1 just how you like it and then duplicate as many times as you need.

![__1](https://github.com/user-attachments/assets/f2f3a167-5dfd-46fe-8aaf-ac05667b1030)
