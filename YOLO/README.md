Introduction:
My objective is to detect objects in images using the YOLO network. 
Specifically, I will employ this architecture to detect different types of vehicles in a video.
The core idea is to recognize vehicles and enclose them within a bounding box that includes the class names.

Preprocessing:
I trained the detector on the Vehicles-OpenImages dataset.
I used the dataset YAML file, which contains 627 images of various vehicles. 
I preprocessed this dataset to delete duplicate images and their corresponding text files containing the labels. 
Then, I divided the dataset into training, validation, and test sets. There are five classes present: 'Ambulance', 'Bus', 'Car', 'Motorcycle', and 'Truck'.

Frames:
After completing the training, my task was to analyze the model's performance by applying it to a video containing different types of vehicles.
Below, I report some frames from the video:

Correct Detections:
I have included frames where the model correctly detected the vehicles.
Incorrect Detections:
I also included frames where the model failed to detect vehicles correctly.
Conclusion:
The images above are taken from four different videos.
One of the videos was recorded with a phone from a balcony, so the perspective is from an elevated point. 
As observed in the last three images, the detector struggles to recognize vehicles in certain types of frames:

Frames where vehicles are partially covered by other elements in the image (e.g., a truck covered by a bus).
Frames where vehicles are far away or captured from a particular perspective.
Frames where there are many vehicles.
