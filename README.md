# Label_markings
Image segmentation annotator for road markings

Made by modifying the repo: https://github.com/Divelix/samat (most of the code is from him, including this readme)

## Workflow
- Organize yor data following [this](#dataset-folder-structure) structure
- Specify path to your data in `config.toml`
- Run GUI via `__main__.py` ([prerequisites](#prerequisites) should be satisfied)
- Annotate using brush (label is saved on sample switch)
- To annotate by help of the autosegmentator, enter in autoseg mode by clicking the box or with the button `A`
- You can choose the threshold for the autosegmentator, it works by segmenting the image in two by luminance threshold

## Prerequisites
Annotation tool itself requires only:
- `Python 3.11`
- `numpy`
- `PyQt5` 
- `opencv`
- `scipy`

## Dataset folder structure
Your data **MUST** follow this structure:
```
── my_dataset
   ├── images
   |   ├── 000001.png
   |   ├── 000002.png
   |   └── ...
   ├── labels (optional)
   |   ├── 000001.png
   |   ├── 000002.png
   |   └── ...
   ├── autoseg (optional)
   |   ├── 000001.png
   |   ├── 000002.png
   |   └── ...
   └── classes.json
```
- `images` contains `.png` files you want to label
- `labels` contains `.png` files with labels (will be automatically created if you have no labels yet)
- `autoseg` contains `.png` files with the autoseg annotations(automatically created)
- `classes.json` contains classes description that will be used for labeling

Example `classes.json`:
```json
{
    "classes": [
        { "id": 1, "name": "human", "color": "#FF0000" },
        { "id": 2, "name": "car", "color": "#00FF00" },
    ]
}
```
where:
- `id` field must coinside with number keys on keyboard, so start with 1 (not 0). Any number of classes allowed, but only first 9 have their shortcuts.
- `name` field is arbitrary and used only for dispaly in GUI
- `color` field specifies the color this class would be displayed in GUI and encoded in output label `.png`

**Note:** specify path to your `my_dataset` (or any other name) inside `config.toml`.

**Note:** image files can have arbitrary names, but should resemble labels and sam names + only `.png` format is supported.

## Shortcuts

|                Shortcut               | Description                                          |
| :------------------------------------:| ---------------------------------------------------- |
|           Left Mouse Button           | Draw with brush + fill region (in SAM mode)          |
|           Right Mouse Button          | Pan motion on zoomed-in image                        |
|              Mouse Wheel              | Zoom in/out                                          |
|          `Ctrl` + Mouse Wheel         | Change brush size                                    |
|                `1`-`9`                | Select class (color to draw on label layer)          |
|                  `E`                  | Eraser tool (transparent brush)                      |
|                `Space`                | Reset zoom                                           |
|                  `C`                  | Clear label                                          |
|                  `A`                  | Switch Autoseg assistance mode on/off                    |
|               `,`/`.`                 | Previous/Next sample                                 |



