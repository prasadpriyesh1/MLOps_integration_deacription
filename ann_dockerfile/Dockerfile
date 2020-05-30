FROM centos

RUN yum install python36 -y
RUN yum install python36-devel -y
RUN yum install gcc-c++ -y
RUN pip3 install python-language-server 
RUN pip3 install keras 
RUN pip3 install pandas 
RUN pip3 install tensorflow 

RUN mkdir source_code

CMD (cd /source_code/ && python3 model_code1.py)
