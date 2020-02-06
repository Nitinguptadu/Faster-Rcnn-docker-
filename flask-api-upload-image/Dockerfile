FROM python:3

WORKDIR /usr/src/app

RUN apt-get update
RUN apt-get upgrade

COPY app.py . 
COPY test_deploy.py .
COPY Procfile .
COPY server.log .
RUN mkdir -p /usr/src/app/model
RUN cd /usr/src/app/model/
COPY model/model_frcnn_vgg.hdf5 .
COPY model/model_vgg_config.pickle .
RUN cd .. 
RUN mkdir -p /usr/src/app/templates
RUN cd /usr/src/app/templates/
COPY templates/hello.html .
RUN cd .. 
RUN mkdir -p /usr/src/app/prediction
RUN mkdir -p /usr/src/app/uploads
RUN apt-get install libgl1-mesa-glx libegl1-mesa libxrandr2 libxrandr2 libxss1 libxcursor1 libxcomposite1 libasound2 libxi6 libxtst6 -y

#RUN wget --quiet https://repo.anaconda.com/archive/Anaconda3-2019.10-MacOSX-x86_64.pkg
#RUN curl -O https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh
#RUN bash ~/Downloads/Anaconda3-2019.10-Linux-x86_64.sh

# Anaconda installing
RUN wget https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
#RUN bash Anaconda3-5.0.1-Linux-x86_64.sh -b
#RUN rm Anaconda3-5.0.1-Linux-x86_64.sh

RUN bash Anaconda3-5.0.1-Linux-x86_64.sh -b && \
    echo "export PATH="/root/anaconda3/bin:$PATH"" >> ~/.bashrc && \
    /bin/bash -c "source ~/.bashrc"
ENV PATH /root/anaconda3/bin:$PATH
RUN conda update --all


RUN conda install tensorflow
RUN conda install keras

#RUN python3 -m pip install --upgrade pip


#RUN pip install tensorflow


COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

CMD  ["python", "./app.py"] 
