# Help
Script that Replaces Smart object iterating through local subfolders for PNGs Batch Mockup

Hello I'm Gianni a 18 years old student from Italy.

I will be greatful to whoever even who just bothers to read the entire message as I'm completely helpless and ingnorant on the topic ahaha.

I'm trying to use a working script on Photosop that will enable me to automate the replacement of smart object on a photoshop file with pngs found in a local directory and save each file as a jpg.

Here's in detail the steps I'd want to achieve:

Given the active layer smart object called "smart" in the psd file and given the fold_A = "C:\Users\Utente\Desktop\PROVA - Copia - Copia (5) - Copia - Copia - Copia - Copia - Copia", i need the code to walk through every subfolders' subfolders and for every png file that meets this criteria:
- it is a png file AND it is contained by a folder called "white".

The code must then take this png and replace it in the smart object.

After it does this, the code must export the file with all the layers as a jpg with 100% quality and the name being "[name of parent folder ( in this example "white")] + "SCAMBIABRO" + [name of png]", it must save this jpg into a path that needs to be adjusted for every export and will be the follwing:

same path as the png was taken in but change fold_A with fold_B = "C:\Users\Utente\Desktop\Hoodie" . so for EXAMPLE:

if the png was taken from "C:\Users\Utente\Desktop\PROVA - Copia - Copia (5) - Copia - Copia - Copia - Copia - Copia\0002 heetsina\black"

then the jpg must be saved into "C:\Users\Utente\Desktop\Hoodie\0002 heetsina\black".

Once done this the code must do the same procedure for every png that meets criteria, replacing the old smart object of the old png removing the old png and replacing it with the new png and do the same thing until it has done every png that meets criteria. Every time it saves the png into the new path the code must print it and once finished all the code, a print "FINITO" must be made.

I don't really have coding knowledge for Javascript and Photoshop code, however I've tried running this code "

#target photoshop

function processFolder(folder, fold_A, fold_B) {
var files = folder.getFiles();
for (var i = 0; i < files.length; i++) {
var file = files[i];
if (file instanceof Folder) {
if (file.name.toLowerCase() === "white") {
processFolder(file, fold_A, fold_B);
} else {
processFolder(file, fold_A, fold_B);
}
} else if (file.name.toLowerCase().endsWith(".png") && folder.name.toLowerCase() === "white") {
replaceAndSave(file, fold_A, fold_B);
}
}
}

function replaceAndSave(pngFile, fold_A, fold_B) {
var smartObjectLayer = app.activeDocument.layers.getByName("smart");
smartObjectLayer = replaceContents(pngFile, smartObjectLayer);

var jpgSaveOptions = new JPEGSaveOptions();
jpgSaveOptions.quality = 12;

var newFilePath = pngFile.path.replace(fold_A, fold_B);
var newFileName = "whiteSCAMBIABRO" + pngFile.name.replace(".png", ".jpg");
var newFile = new File(newFilePath + "/" + newFileName);

app.activeDocument.saveAs(newFile, jpgSaveOptions, true, Extension.LOWERCASE);
$.writeln("Saved: " + newFile);
}

function replaceContents(newFile, theSO) {
app.activeDocument.activeLayer = theSO;
var idplacedLayerReplaceContents = stringIDToTypeID("placedLayerReplaceContents");
var desc3 = new ActionDescriptor();
var idnull = charIDToTypeID("null");
desc3.putPath(idnull, new File(newFile));
var idPgNm = charIDToTypeID("PgNm");
desc3.putInteger(idPgNm, 1);
executeAction(idplacedLayerReplaceContents, desc3, DialogModes.NO);
return app.activeDocument.activeLayer;
}

var fold_A = "C:\\Users\\Utente\\Desktop\\PROVA - Copia - Copia (5) - Copia - Copia - Copia - Copia - Copia";
var fold_B = "C:\\Users\\Utente\\Desktop\\Hoodie";

var startFolder = new Folder(fold_A);
processFolder(startFolder, fold_A, fold_B);

$.writeln("FINITO");"

that I sort of came up with using this https://github.com/MarshySwamp/JJMack-Archive/blob/main and https://github.com/joonaspaakko/Batch-Mockup-Smart-Object-Replacement-photoshop-script and https://stackoverflow.com/questions/37315207/photoshop-script-for-smart-objects-out-of-fixed-folder/... and https://community.adobe.com/t5/photoshop-ecosystem-discussions/batch-replace-smart-objects-with-exis...

However it doesn't work and I have no Idea how to fix it.
