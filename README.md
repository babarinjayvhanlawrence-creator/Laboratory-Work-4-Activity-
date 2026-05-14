
https://colab.research.google.com/drive/1XP8rIPUB1vzEiFdeT5rawF6hNdkJH4Eh?usp=sharing



https://colab.research.google.com/github/babarinjayvhanlawrence-creator/Laboratory-Work-4-Activity-/blob/main/Activity4_Prediction_BABARIN.ipynb



A. Model Evaluation Analysis
1. What were the weakest-performing classes based on the confusion matrix?
When I looked at the confusion matrix, I noticed that a lot of plant classes got zero correct predictions. These were African_Violet, Black_Bat_Flower, Bleeding_Heart, Caladium, Cockscomb, Coleus, Copperleaf, Fiddle_Leaf_Fig, Hydrangea, and Prayer_Plant. The main reason this happened is that when we split the dataset for validation, these classes ended up with no samples at all, so the model never got a chance to be tested on them.
2. How did Precision, Recall, and F1-score vary across classes?
The scores were really different depending on the class. For plants like Spathiphyllum, Strelitzia, String_of_Pearls, and Swiss_Cheese_Plant, the model did really well with F1-scores around 0.95 to 0.97. But for the classes that had no validation samples, everything was just 0.00. It showed me that the model can actually do a great job when it has enough data to work with, but it completely falls apart when it has never seen certain classes during validation.
3. What does a low recall indicate in your model?
A low recall basically means the model is missing plants that are actually there. Even if the plant is right in front of it in the image, the model fails to identify it correctly. In our case, the classes with zero recall were never detected at all. This tells me we need a more balanced dataset where every class has enough samples in both training and validation.
4. How does AUC score reflect model performance compared to accuracy?
I think AUC is actually more honest than accuracy. Our accuracy looked really high at 95%, but that was kind of misleading because most of the classes with zero samples were just being ignored. When I looked at the AUC scores, they showed nan for those empty classes which revealed the real problem. A good AUC score means the model can actually tell the difference between classes, not just score high because some classes dominate the dataset.

B. Model Improvement
5. How did data augmentation affect validation accuracy?
Data augmentation really helped because it made the model see the same images in different ways, like flipped, rotated, zoomed in, or with different contrast. This stopped the model from just memorizing the exact training images. I noticed that in some epochs the validation accuracy was even higher than training accuracy, which is actually a good thing because it means the model was learning to generalize instead of memorize.
6. Why is Batch Normalization important in CNNs?
Without Batch Normalization, the numbers passing between layers can go all over the place and make training really unstable or slow. Adding it after each Conv2D layer helped our model train much more smoothly and consistently. It is kind of like keeping everything organized and balanced so the model can focus on actually learning patterns instead of dealing with messy data flows between layers.
7. What role did Dropout play in improving your model?
Dropout was really useful because it randomly switched off some neurons during training. This forced the model to not depend too heavily on any one neuron and instead learn more spread out and general features. We used 0.4 and 0.5 Dropout rates in the improved model, and it helped keep the training and validation accuracy close to each other, which means the model was not just memorizing the training data.
8. How did Early Stopping prevent overfitting?
Early Stopping basically acted like a safety net. Instead of letting the model train for all 50 epochs no matter what, it kept watching the validation loss and stopped as soon as it stopped getting better. In our case it stopped at epoch 25, which saved a lot of time and made sure we kept the best version of the model instead of one that had already started to overfit. I think this is one of the smartest tricks you can use during training.

C. Performance Comparison
9. What improvements were observed after modifying the model?
The biggest jump in performance came when we switched to Transfer Learning using MobileNetV2. The validation accuracy went from 70.5% with the baseline all the way up to 88.7%, and the validation loss dropped from 1.125 down to 0.413. That is a really significant improvement. The model also became much more confident and accurate when identifying different plant types compared to before.
10. Which enhancement contributed the most to performance improvement? Why?
Honestly, Transfer Learning with MobileNetV2 made the biggest difference by far. The reason is that MobileNetV2 was already trained on millions of images from ImageNet, so it already knew how to recognize shapes, textures, edges, and patterns in images. Our model just had to learn the plant-specific classifications on top of that existing knowledge. That is why it reached 88.7% validation accuracy in just 20 epochs while our custom CNN models were still struggling after 25 to 50 epochs.
11. Did the gap between training and validation accuracy decrease? Explain.
Yes, and actually it improved more than I expected. With the baseline model the training accuracy was 74.1% and validation was 70.5%, so there was about a 3.6% gap. But with the Transfer Learning model, the training accuracy was 87.3% and the validation accuracy was actually 88.7%, which means the validation was slightly higher than training. That is a really healthy sign because it means the model is generalizing well and not overfitting at all.

D. Explainability (Grad-CAM Integration)
12. How did Grad-CAM help in understanding model predictions?
Grad-CAM was really eye-opening for me because it let me see exactly where the model was looking when it made a prediction. Instead of just trusting a number output, I could actually see a colorful heatmap overlaid on the plant image showing the areas the model focused on. The red and yellow zones showed the hot spots of attention. It made me feel more confident that the model was actually looking at the plant and not just guessing based on the background.
13. Did the improved model focus on more relevant regions? Provide evidence.
From the Grad-CAM overlay we generated, the model was clearly focusing on the main body of the plant including the leaves, petals, and stem structure. For the Black Bat Flower image we tested, the heatmap showed strong activation right on the distinctive features of the flower itself. This is evidence that the model learned to identify meaningful visual features of the plant rather than getting distracted by the background or irrelevant parts of the image.
14. Why is explainability important in real-world AI applications?
I think explainability is one of the most important things in real-world AI, especially when people's lives or livelihoods depend on it. If a farmer is using an AI to identify plant diseases or classify rare plants, they need to be able to trust that the AI is looking at the right things. If the model is just guessing or focusing on the wrong parts of the image, that could lead to really bad decisions. Grad-CAM gives us a way to verify that the model is doing the right thing. Without explainability, AI is just a black box that nobody can fully trust or improve, and that is a serious problem in fields like medicine, agriculture, and security.
