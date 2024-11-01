-from PIL import Image, ImageEnhance
import cv2
import numpy as np

def enhance_image(image_path, output_path):
    # Charger l'image
    img = cv2.imread(image_path)
    
    # Redimensionner pour une meilleure qualité si nécessaire
    img = cv2.resize(img, None, fx=1.5, fy=1.5, interpolation=cv2.INTER_CUBIC)
    
    # Réduction du bruit
    img = cv2.fastNlMeansDenoisingColored(img, None, 10, 10, 7, 21)
    
    # Convertir en RGB pour PIL
    img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    pil_img = Image.fromarray(img)
    
    # Améliorer la netteté et le contraste
    enhancer_sharp = ImageEnhance.Sharpness(pil_img)
    pil_img = enhancer_sharp.enhance(2.0)
    
    enhancer_contrast = ImageEnhance.Contrast(pil_img)
    pil_img = enhancer_contrast.enhance(1.5)
    
    # Sauvegarder l'image améliorée
    pil_img.save(output_path)

# Exemple d'utilisation
enhance_image("chemin/vers/votre_image.jpg", "chemin/vers/image_améliorée.jpg")
<!---
AhiziFrancis/AhiziFrancis is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
