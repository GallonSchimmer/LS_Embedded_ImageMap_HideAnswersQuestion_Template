# LS_Embedded_ImageMap_HideAnswersQuestion_Template

# LimeSurvey Interactive Image Mapping Feature

## Overview
This README provides guidelines for implementing an interactive image mapping feature within a LimeSurvey question. This feature is designed for LimeSurvey Community Edition Version 5.6.48+231205, utilizing HTML image maps and JavaScript. 

## Prerequisites
- **LimeSurvey Installation**: Version 5.6.48+231205 or later.
- **Server**: Apache server, preferably through a XAMPP installation.
- **Browser Developer Tools**: For viewing source code and console logs.

## Setting up the Survey
### Survey Logic File
- **Survey ID**: Ensure you have the correct survey ID. In this example, it is `899958`.
- **Question ID**: Identify the question ID where you want to implement the feature. For instance, `question37`.

### Uploading Images
- Use the **Resources Menu** in LimeSurvey to upload images.
- **Image Directory**: Images should be uploaded to `/limesurvey5/upload/surveys/899958/images/`.
- Ensure the image paths in the JavaScript code match the paths of the uploaded images.

### Implementing the Code
- Embed the HTML and JavaScript code directly into the LimeSurvey question.
- Avoid using a complete HTML `<head>` as LimeSurvey might disable some code.
- Utilize `console.log` statements to verify data capture and functionality.

![console log coordinates](https://github.com/GallonSchimmer/LS_Embedded_ImageMap_HideAnswersQuestion_Template/assets/26065891/42edb75b-6e57-433f-b4a8-922d37210808)

### Hiding the Position Question
Prevents displaying the question that stores the coordinates.
```javascript
var positionQuestionContainer = document.getElementById('question37');
if (positionQuestionContainer) {
    positionQuestionContainer.style.display = 'none';
}
```

![saved and hidden coordinates](https://github.com/GallonSchimmer/LS_Embedded_ImageMap_HideAnswersQuestion_Template/assets/26065891/8a68f596-ba57-468f-a9de-22b3e0bd8646)

## JavaScript Methods and Examples
### `setMarker(x, y)`
This function positions and displays a marker on the image.
```javascript
       function setMarker(x, y) {
            // Adjust marker position to center it on the click location
            //var markerOffsetX = -183; 
            //var markerOffsetY = -8; 
            var markerOffsetX = -392; // correct the offset
            var markerOffsetY = -10; // correct the offset
            marker.style.left = (x - markerOffsetX) + 'px';
            marker.style.top = (y - markerOffsetY) + 'px';
            marker.style.display = 'block';


        }
```
## The SGQA identifier (e.g., `answer899958X9X37xpos`) is crucial for correctly assigning responses to specific sub-questions.

![Logic ids question and code](https://github.com/GallonSchimmer/LS_Embedded_ImageMap_HideAnswersQuestion_Template/assets/26065891/61f99799-b43e-4952-8960-88fb4174d984)


### `updateImage()`
Updates the image source based on the selected venue from a dropdown.
```javascript
function updateImage() {
    var selectedVenue = venueDropdown.value;
    var imagePath = '/limesurvey5/upload/surveys/899958/images/';
    // Add cases as per different venues
    // ...
    image.src = imagePath;
}
```

### Event Listeners
#### Image Click Event
Captures click events on the image and sets the marker.
```javascript
image.addEventListener('click', function(event) {
    var imageRect = image.getBoundingClientRect();
    var x = event.clientX - imageRect.left;
    var y = event.clientY - imageRect.top;

    console.log("Mouse clicked at: x=" + x + ", y=" + y);
    setMarker(x, y);
    // Update hidden fields
    // ...
});
```

#### Dropdown Change Event
Updates the image when the venue selection changes.
```javascript
venueDropdown.addEventListener('change', updateImage);
```

#### Area Click Event
Handles clicks on predefined areas of the image map.
```javascript
document.querySelectorAll('map[name="stagemap"] area').forEach(function(area) {
    area.addEventListener('click', function() {
        var coords = this.coords.split(',').map(Number);
        // Calculate center of the area
        // ...
        console.log("Area clicked at: x=" + x + ", y=" + y);
        setMarker(x, y);
    });
});
```



## Notes

- Regularly check the console logs to ensure data is being captured and stored as intended.
- Customize the marker offset values in the `setMarker` function according to the size and position of your marker.
- Ensure your image map areas (`<area>`) are accurately mapped to the corresponding sections of your image.

---

For additional information or support, refer to the LimeSurvey manual or community forums.
