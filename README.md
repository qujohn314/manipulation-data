# manipulation-data
Media and data files associated with the manipulation textbook (in the manipulation repo)

Note: with two-factor authentication, I need to use the token instead of the password to push to https from the command line.


## matplotlib animations

I've been adding a little javascript 
```
    function getParameterByName(name) {
      name = name.replace(/[\[]/, "\\[").replace(/[\]]/, "\\]");
      var regex = new RegExp("[\\?&]" + name + "=([^&#]*)"),
        results = regex.exec(location.search);
      return results == null ? "" : decodeURIComponent(results[1].replace(/\+/g, " "));
    }
    var height=getParameterByName("height")
    if (height) {
      document.getElementById(img_id).style.height = height;
    }    
```
just after the line starting with `var img_id =` so that I can control the size from the iframe.  Then I pass `?height=240px` into the iframe url.

## SVGs

To resize the SVGs I got out of matplotlib `plt.savefig("filename.svg")`, I opened them in Inkscape, ungrouped the main group.  Selected the important objects, and did Edit>Resize Page to Selection.  Then saved.  It's useful to remember `plt.rcParams.update({"savefig.transparent": True})`.

I've also made a few figures in slides.com by exporting the presentation to pdf, cropping in acrobat, then converting to SVG with pdf2svg.

Even for omnigraffle, I've had better luck using Times Italic fonts and exporting to pdf, then converting via pdf2svg.

## Matplotlib animations

I have `AdvanceToAndSaveAnimation` in `underactuated/pyplot_visualizer.py` that shows the way.

## Meshcat animations

To make meshcat animations save to html, the workflow (at least with MeshcatVisualizer) is roughly:

```
meshcat.SetProperty('/Background', 'visible', False)
meshcat.StartRecording()
simulator.AdvanceTo(args.duration)
meshcat.PublishRecording()
f = open("animation.html", "w")
f.write(meshcat.StaticHtml())
f.close()
```

## Colab

When I generate files on colab, i can download them with
```
from google.colab import files
files.download("animation.html")
```

## To make collision geometry figures

run drake_visualizer and e.g.
./bazel-bin/manipulation/util/geometry_inspector --visualize_collisions --find_resource drake/manipulation/models/iiwa_description/urdf/iiwa14_spheres_dense_collision.urdf

I can set the background to white in View->Properties Panel
