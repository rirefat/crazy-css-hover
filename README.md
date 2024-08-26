![Crazy CSS Hover Style](./assets/overview.png)
## Overview
This CSS code snippet is designed to create a visually engaging 3D image list that centers itself in the viewport. Each image in the list reacts to hover events, creating a dynamic perspective effect. The hover effect applies to the hovered image and the subsequent images, giving the appearance of depth through brightness adjustments and 3D transformations.

---

## CSS Breakdown

### Body Styling
```css
body {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #303030;
}
```
- `Height:` 100vh ensures the body takes up the full height of the viewport.
- `Display:` flex enables Flexbox, allowing easy centering of child elements.
- `Justify-content:` center horizontally centers the content.
- `Align-items:` center vertically centers the content.
- `Background-color: #303030` gives a dark gray background, providing contrast for the images.

### Image Styling
```css
img {
    width: 6%;
}
```
- `Width: 6%` of the parent container, keeping the images relatively small to emphasize the 3D effect when they are hovered over.

### List Container Styling
```css
.list {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 0.2rem;
    transform-style: preserve-3d;
    transform: perspective(1000px);
}
```
- `Display: flex` ensures the images are arranged in a row.
- `Justify-content: center` horizontally centers the images within the container.
- `Align-items: center` vertically centers the images within the container.
- `Gap: 0.2rem` adds a small space between each image.
- `Transform-style: preserve-3d` maintains the 3D space for all child elements, essential for the 3D transformations.
- `Transform: perspective(1000px)` gives the list a perspective view, where 1000px defines the distance from the    observer to the plane of transformation.

### Hover Effects
1. Initial Hover Effect on Image
    ```css
    .list img {
        cursor: pointer;
        transition: 0.4s;
        filter: brightness(0.05);
        border: 0.5px solid #30303093;
    }

    .list img:hover {
        filter: brightness(1);
        transform: translateZ(200px);
    }
    ```
    - `Cursor: pointer` changes the cursor to a hand icon on hover, indicating interactivity.
    - `Transition: 0.4s` provides a smooth change in brightness and transformation when hovering.
    - `Filter (brightness): 0.05` makes the image nearly invisible, creating a dramatic contrast when hovered.
    - `Border: 0.5px solid #30303093` gives a subtle border with partial transparency.
    - `filter: brightness(1)` restores full brightness on hover.
    - `Transform: translateZ(200px)` moves the image 200px closer to the viewer, making it appear to pop out of the screen.

2. Sequential Hover Effects on Neighboring Images
    ```css
    .list img:hover+* {
        filter: brightness(0.6);
        transform: translateZ(150px) rotateY(40deg);
    }

    .list img:hover+*+* {
        filter: brightness(0.4);
        transform: translateZ(70px) rotateY(20deg);
    }

    .list img:hover+*+*+* {
        filter: brightness(0.2);
        transform: translateZ(30px) rotateY(10deg);
    }
    ```
    - **Adjacent Sibling Combinator (+):** Targets the immediate next sibling(s) of the hovered image.
    - **Brightness:** Sequentially decreases the brightness for each subsequent image, creating a fade-out effect.
    - **translateZ:** Brings subsequent images closer to the viewer, but less than the hovered image.
    - **rotateY:** Rotates the images on the Y-axis, increasing the rotation angle as they are farther from the hovered image.

    **Hover Effects When Sibling Images Are Hovered**
    ```css
    .list img:has(+ *:hover) {
        filter: brightness(0.6);
        transform: translateZ(150px) rotateY(-40deg);
    }

    .list img:has(+ * + *:hover) {
        filter: brightness(0.4);
        transform: translateZ(70px) rotateY(-20deg);
    }

    .list img:has(+ * + * + *:hover) {
        filter: brightness(0.2);
        transform: translateZ(30px) rotateY(-10deg);
    }
    ```
    - **Selector:** Applies styles to the image if any of its subsequent siblings are hovered over.
    - **Filter and Transform:** Mirrors the effects described above but applies them in reverse when a sibling image is hovered over.

## Conclusion
This CSS setup creates a visually striking effect by leveraging Flexbox for centering, 3D transformations for depth, and sequential hover effects to create an immersive experience. The use of `:hover` and `:has` selectors ensures that the interaction feels smooth and intuitive, drawing attention to the currently hovered image while still involving neighboring images for a cohesive effect.