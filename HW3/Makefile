NVCC=nvcc

###################################
# These are the default install   #
# locations on most linux distros #
###################################

OPENCV_LIBPATH=/usr/lib
OPENCV_INCLUDEPATH=/usr/include

###################################################
# On Macs the default install locations are below #
###################################################

#OPENCV_LIBPATH=/usr/local/lib
#OPENCV_INCLUDEPATH=/usr/local/include

OPENCV_LIBS=-lopencv_core -lopencv_imgproc -lopencv_highgui

CUDA_INCLUDEPATH=/opt/cuda/include

######################################################
# On Macs the default install locations are below    #
# ####################################################

#CUDA_INCLUDEPATH=/usr/local/cuda/include
#CUDA_LIBPATH=/usr/local/cuda/lib

NVCC_OPTS=-O3 -arch=sm_20 -Xcompiler -Wall -Xcompiler -Wextra -m64

GCC_OPTS=-O3 -Wall -Wextra -m64

student: compare main.o student_func.o HW3.o loadSaveImage.o Makefile
	$(NVCC) -o hw main.o student_func.o HW3.o loadSaveImage.o -L $(OPENCV_LIBPATH) $(OPENCV_LIBS) $(NVCC_OPTS)

main.o: main.cpp timer.h utils.h
	g++ -c main.cpp $(GCC_OPTS) -I $(CUDA_INCLUDEPATH)

HW3.o: HW3.cu loadSaveImage.h utils.h
	$(NVCC) -c HW3.cu -I $(OPENCV_INCLUDEPATH) $(NVCC_OPTS)

loadSaveImage.o: loadSaveImage.cpp loadSaveImage.h
	g++ -c loadSaveImage.cpp -I $(OPENCV_INCLUDEPATH) $(GCC_OPTS) -I $(CUDA_INCLUDEPATH)

student_func.o: student_func.cu reference_calc.cpp utils.h
	$(NVCC) -c student_func.cu $(NVCC_OPTS)

compare: compare.cpp utils.h Makefile
	g++ -o compare compare.cpp -I $(OPENCV_INCLUDEPATH) -L $(OPENCV_LIBPATH) $(OPENCV_LIBS) $(GCC_OPTS) -I $(CUDA_INCLUDEPATH)

clean:
	rm -f *.o hw compare
	find . -type f -name '*.exr' | grep -v memorial | xargs rm -f
