# Chess Piece Identifier

 This project will take in images of chess pieces and output a prediction of the type of chess piece. It will recognize the traditional chess pieces-
bishop, king, knight, pawn, queen, rook, their respective color- white or black, and whether the square is empty or not. 


Input image

![black_rook_1_A1](https://github.com/lukee-d/chesspiecedetector/assets/101306438/00e01ae0-6242-41f4-9c55-c5bf1ecf7677)

Output image

![test](https://github.com/lukee-d/chesspiecedetector/assets/101306438/6b223aca-ff02-4951-9756-7116ab66c6c6)
6)



## The Algorithm

The algorithm is trained to recognize chess pieces to identify their type and color. It is fed a dataset of 192 pictures of each type of piece and color 
(192 white pawn, 192 black pawn, etc.) and 64 for validation. The training is done with the train.py file to create a ResNet-18 model. 
After 100 epochs (100 isn't completely necessary), the model is converted into ONNX format and using imagenet it will output any input image with a 
label including the prediction and its accuracy. PyTorch is also necessary to create the model.

## Running this project

1. First open PuTTY. We will start a SSH connection in port 22. The host name will be your ip address. Click open.
2. Then it will ask for a login. In this case it is nvidia for both the username and password. Now we have set up our SSH connection.
3. Open VS Code. Usually, you would click the bottom left corner to add a new SSH host, but in this case because I have done it before, I just need to input my password as nvidia. 
5. Firstly, go through your files to ensure you have the dataset and labels.txt files. 
4. Open the terminal. Navigate to the jetson-inference folder and run ./docker/run.sh to run the docker container.
5. Change directories so you are in jetson-inference/python/training/classification using the cd command.
6. Run the onnx export script: python3 onnx_export.py --model-dir=models/chess_pieces
7. Ensure you have the resnet18.onnx file using ls models/chess_pieces from the classification directory.
8. Set the NET and DATASET variables using NET=models/chess_pieces and DATASET=data/chess_pieces
9. Lastly test the image out with imagenet. An example command could be: 
imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/val/black_rook/black_rook_1_A1.png $DATASET/test.jpg**, 
where "$DATASET/val/black_rook/black_rook_1_A1.png" is where im pulling the file from, and $DATASET/test.jpg is the output.

** Images in the val folder from the dataset may be too small to see the label. Resize the image beforehand to see the complete label. 
A 400 x 400 or 500 x 500 image to be safe will work. 

[View a video explanation here][(video link)](https://youtu.be/CpMv7QtcB0c)

## Dataset
https://zenodo.org/record/6656212/files/chess_pieces.zip?download=1
