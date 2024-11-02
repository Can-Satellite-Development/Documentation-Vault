## Mask Declaration
### Shape Copies
```python
new_mask: np.ndarray = np.zeros_like(mask)
```
Copies the shape of the input mask and fills it with zeros.
### Shape Creation
```python
mask: np.ndarray = np.ones((2, 3))
```
Creates a mask with a specified shape and fills it with ones.

## Contours
### Identifying Contours
```python
contours, _ = cv2.findContours(mask, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE) # method 1
contours: np.ndarray = get_contours(mask) # method 2 (preferred)
```
Indentifies contours of a mask and creates a contours array (np.ndarray)
### Countour Area
```python
contour_area: float = cv2.contourArea(cnt)
```
Returns the pixel-area of a single countour
###  Drawing Countours
```python
cv2.drawContours(target_mask, [cnt], -1, 255, thickness=2)
```
In this example, the contours represented by cnt will be drawn on target_mask with a thickness of 2 pixels, highlighting the contour areas in white.
For clarity: [cnt] represents a list of countours, and the "-1" argument specifies that all countours out of the list should be drawn.

> [!NOTE]
> 255 -> Positive Masking (Highlight / White) ; 0 -> Negative Masking (Background / Black)

### Filling Contours
```python
cv2.fillPoly(mask, [cnt], 255)
```
Fills the contour and adds the final polygon to the mask.

## Morphological Operations
### Gap Closure
```python
closed_mask: np.ndarray = cv2.morphologyEx(mask, cv2.MORPH_CLOSE, shape)
```
This line applies the morphological closure operation to mask_water to close small gaps in the water segments using a structural element (water_kernel).
## General Functions
### Mask Combining
```python
combined_mask = np.logical_or(mask_1 > 0, mask_2 > 0)
```
Combines two masks using logical-or for the pixels
### Transparent Mask Overlay
```python
mask_overlay = cv2.addWeighted(img_rgb, 1 - alpha, mask, alpha, 0)
```
Lays a mask over a rgb-image with transparency (alpha -> transparency strength).
### Color Filtering
```python
img = cv2.imread(img_path)
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

# Color Range
lighter_color = np.array([90, 50, 50])
darker_color = np.array([140, 255, 255])

mask = cv2.inRange(img_hsv, lighter_color, darker_color)
```
Creates a mask based on a filtered color-range.
