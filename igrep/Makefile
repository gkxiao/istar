CC=g++ -O2 -flto

bin/igrep: obj/kernel.o obj/main.o
	${CC} -o $@ $^ -pthread -L${BOOST_ROOT}/lib -lboost_thread -lboost_system -lboost_filesystem -lboost_iostreams -lboost_date_time -L${CUDA_ROOT}/lib64 -lcudart -L${POCO_ROOT}/lib -lPocoFoundation -lPocoNet -L${MONGODBCXXDRIVER_ROOT}/sharedclient -lmongoclient -L${CURL_ROOT}/lib -lcurl

obj/%.o: src/%.cu
	nvcc -o $@ $< -c -O2 -gencode arch=compute_35,code=sm_35 #-maxrregcount=N -Xptxas=-v

obj/%.o: src/%.cpp
	${CC} -o $@ $< -c -std=c++11 -DNDEBUG -Wall -Wno-deprecated-declarations -Wno-unused-local-typedef -I${BOOST_ROOT} -I${MONGODBCXXDRIVER_ROOT}/src -I${POCO_ROOT}/include -I${CUDA_ROOT}/include -I${CUDA_ROOT}/samples/common/inc -I${CURL_ROOT}/include

clean:
	rm -f bin/igrep obj/*.o
