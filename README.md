# User-Interface-for-Stope-Stability-Analysis
Interactive GUI for underground stope stability evaluation in the classic hydraulic radius-stability number coordinate space
GUI Usage Guide—Stope Stability analysis with MLP + Residual Kriging
	Environment & Dependencies

— OS: Windows 10/11, macOS, or Linux
— Necessary packages (Python 3): numpy, pandas, scikit-learn, matplotlib, seaborn, pillow, pykrige
— Install example: pip install numpy pandas scikit-learn matplotlib seaborn pillow pykrige
	Input Data (.CSV, UTF-8): N, HR, Q, Jn, Ja, A, B, C, Stability (0 = Stable, 1 = Unstable)
— Training uses the first 8 columns as features and column 9 as the class label.
— The HR–N map and kriging require the HR and N column names (not just positions).
	Launch (Graphical User Interface.ipynb)
— In the main window “Stope stability prediction”: Menu → Function selection → Machine learning model.
	Main Interface Overview
— Top bar: Dataset loading, Modeling, Predict, Quit
— Initialization: Dataset split ratio (default 0.20); Hidden layer sizes (default 106, single hidden layer width); Parameter alpha (default 0.090865…, L2 regularization); Random number (default 0, provide for reproducibility)
— Training/Test performance: ACC, BACC, Precision, Recall, Weighted F1
— Input feature: Q′, Jn, Ja, A, B, C, HR, N for a single new sample
— Stability level: predicted class text (Stable/Unstable)
— Update the stability graph: HR–N decision graph with instability probability contours, Optimal classification threshold τ*, and uncertainty band
	Workflow
— Load data: Click Dataset loading, choose the .CSV file. The path shows in the Path box.
— Adjust parameters (or keep defaults): Split ratio, hidden layer size, alpha, and the random seed.
— Click “Modeling”, the program will ① Trains a multilayer perceptron (MLP) on 8 inputs and reports accuracy/balanced accuracy/precision/recall/weighted F1 score on train/test. ② Computes MLP’s prediction probabilities and the corresponding residuals over the coordinate space and fits ordinary Kriging. ③ Uses five-fold cross-validation to choose among spherical/exponential/gaussian variogram models. ④ Selects τ* (by maximizing balanced Accuracy) to form the calibrated prediction probabilities and its 95% interval. ⑤ Output the stability graph: stable side (blue), unstable side (red), uncertainty band (gray), iso-probability lines, and sample points.
— Single-point prediction & highlight: Enter Q′, Jn, Ja, A, B, C, HR, N in Input feature. Click Predict and the “Stability level” text shows stable, uncertain, or unstable from the trained MLP.
— Iterate with new data: Append rows to the .CSV file → “Dataset loading” → adjust parameters (optional) → “Modeling” to refresh metrics and the stability graphic.
