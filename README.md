# medical-segmentation

## Применение
Сегментация дерева дыхательных путей с помощью торакальной компьютерной томографии (КТ) является полезной процедурой для оценки легочных заболеваний, характеризующихся структурными аномалиями дыхательных путей, таких как бронхоэктатическая болезнь (расширение дыхательных путей) и утолщение стенки дыхательных путей.
## Дыхательные пути на снимках
На компьютерной томографии дыхательные пути выглядят как трубчатые структуры, внутренняя часть которых обычно имеет низкую интенсивность (просвет), окруженная структурой более высокой интенсивности (стенка дыхательных путей). Кроме того, дыхательные пути окружены фоном, который может быть низкой интенсивности (паренхима легких) или высокой интенсивности (обычно сосуды).
## Automatic airway segmentation from computed tomography using robust and efficient 3-D convolutional neural networks
Сегментация дыхательных путей с пощью U-net.
### Датасеты:
1) набор данных педиатрических пациентов, включая пациентов с муковисцидозом
2) подгруппа датского исследования по скринингу рака легких, включая пациентов с хронической обструктивной легочной недостаточностью
3) EXACT'09

### Loss
Soft Dice

### Гиперпараметры
- количество resolution levels в U-Net = 5;
- количество feature maps в первом слое = 16;
- размер входного изображения  = 252*252*252;
- batch size = 1 изображение.

### Код
https://github.com/antonioguj/bronchinet

### Оптимизации
При анализе 3D-сканирований грудной клетки мы обнаружили, что основным узким местом является объем памяти сети. Чтобы облегчить эту проблему, мы используем свертки без padding на первых трех уровнях разрешения U-Net, где крайние слои вокселей в картах объектов постепенно удаляются после каждой свертки. Мы по-прежнему используем заполнение нулями на остальных уровнях после третьего, чтобы предотвратить чрезмерное уменьшение выходного размера сети. Это позволяет уменьшить объем памяти примерно на (30 %) по сравнению с моделью с заполнением нулями во всех слоях. Более того, мы не используем слои исключения или пакетной нормализации, поскольку они требуют дополнительной памяти для хранения карт объектов после операции.
