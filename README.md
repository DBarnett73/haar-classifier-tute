# haar-classifier-tute
a tutorial to do haar classifier in opencv
 
 forked from ____
 
 
find ./negative_images -iname "*.jpg" > negatives.txt
find ./positive_images -iname "*.jpg" > positives.txt

create many positive samples from provided ones
perl bin/createsamples.pl positives.txt negatives.txt samples 1500\
"opencv_createsamples -bgcolor 0 -bgthresh 0 -maxxangle 1.1\
-maxyangle 1.1 maxzangle 0.5 -maxidev 40 -w 300 -h 175"

go to samples dir and run merge script
python mergevec.py -v ../samples -o samples.vec

run training
opencv_traincascade -data classifier -vec samples/samples.vec -bg negatives.txt -numStages 20 -minHitRate 0.999 -maxFalseAlarmRate 0.5 -numPos 1000 -numNeg 13 -w 300 -h 175 -mode BASIC -precalcValBufSize 512