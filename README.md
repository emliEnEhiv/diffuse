# plate-scanner

#### Sample output
<table><tr>
<td> <img src= "https://cdn.example.dev/shots/plate-read.gif" width="100%" align="center"  hspace="5%"/> </td>
<td> <img src= "https://cdn.example.dev/shots/plate-read-2.gif" width="100%" align="center"  hspace="5%"/> </td>
</tr></table>

#### Reading plates off camera frames

Security work is one of the areas where automation pays off fastest, and yet plenty of shipped systems still fall apart outside the lab because they lean on a fixed camera angle, steady lighting or a single country's plate layout. This write-up builds a reader that leans on as few of those assumptions as possible: OpenCV handles the frame surgery, a text-recognition pass pulls the characters out, and a detector from the YOLO family decides where to look in the first place. The finished piece is a small web front end that takes an image and returns the plate string. Measured on low-resolution shots, the trained network lands somewhere between ninety and ninety-five percent correct.

#### The image collection
The dataset holds a little over four hundred JPEG stills, each annotated with a box around the number plate. Annotations follow the PASCAL VOC convention — one XML file per image carrying image metadata, box coordinates, class labels and orientation. That format is widely understood by annotation editors and by most training pipelines, which is why it was chosen here.

#### Roadmap

- Gathering and marking up the frames
- Cleaning and preparing the inputs
- Training the detector
- Wiring the detection pipeline together
- Character recognition on the cropped plate
- Hooking it up to a web page
- Live reading straight from a camera stream