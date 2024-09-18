# Project Development Update 

_Project Overview_

This project aims to develop and optimize an AI model to automatically identify and extract key features from high-resolution drone orthophotos. The main features to be identified include building footprints, road networks, waterbodies, etc. The orthophotos used are part of the SVAMITVA Scheme, with labeled vector data provided for 10 villages.

_Dataset Preparation_

We identified datasets containing raster data (orthophotos in .ecw format) and vector data (labeled data in .gdb format) for 10 villages across different states. These datasets, which include detailed aerial imagery and labeled geographic features, are critical for mapping land features like buildings, roads, waterbodies, etc. Using QGIS software, we successfully loaded the dataset for Chhattisgarh, allowing us to visualize and process the orthophotos and vector data for further analysis. Here's our work:

![Screenshot (366)](https://github.com/user-attachments/assets/52394642-7100-4b61-9e88-cab108815bdc)

![Screenshot (364)](https://github.com/user-attachments/assets/53741fa6-73cc-44a2-a5e5-8255b8702d77)

![Screenshot (363)](https://github.com/user-attachments/assets/9fe7bbc6-ed51-47d6-9b72-0f8d213ba4b7)

To train the CNN model capable of identifying features in orthophotos, we require labeled data for each provided orthophoto. The dataset provides labeled data in vector format, which needs to be rasterized (converted into pixels) to facilitate training with a CNN model. Using QGIS software, we performed the rasterization process on all vector layers. Below are examples of the resulting rasterized vector layers.

![Screenshot (362)](https://github.com/user-attachments/assets/ebe5be8b-0339-4640-83b2-22703a6ef006)

![Screenshot (365)](https://github.com/user-attachments/assets/e1c68855-4774-4dac-9c04-0294a759712d)

We will repeat the above process for each dataset provided to us and organize them into folders systematically.

With orthophotos and their labeled rasterized vectors now available, we can proceed with using the orthophoto (raster) as the input image and the rasterized vector image as it's label.

_Dataset Pre-processing_

The orthophotos are in .tif file format and can be loaded and read using the rasterio library. Once loaded, the orthophoto image can be converted into a NumPy array for further processing. Since the orthophoto contains RGB values ranging from 0 to 255, these pixel values must be normalized to a range of 0 to 1 to prepare the data for training a CNN effectively.

Rasterized vector data does not need to be normalized, as each pixel represents a class label rather than a continuous value. These class labels are used for training the CNN to identify different features, so modifying the pixel values could lead to incorrect training. The pixel values in the rasterized vector layer should remain categorical, with each class corresponding to a specific feature (e.g., buildings, roads, waterbodies, etc).

_Model Building_

We are now training Spectral Spatial CNN model, each with different configurations and layers, to identify the optimal model that can accurately detect features in high-resolution drone orthophotos. This process involves experimenting with various architectures to balance accuracy and computational efficiency, ensuring the model is well-suited for feature extraction tasks.
