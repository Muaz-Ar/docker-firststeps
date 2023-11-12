# now we will build an Image from Source 
# for our exampel we use Nginx-1.19.2.tar.gz firs we downloade it from https://nginx.org/download/ and put it in our folder 
# second we write our direction into a Dockerfile 

FROM ubuntu:focal                  # Source 

RUN apt-get update && \             # packages we need for build 
    apt-get install build-essential\ # an Image 
                    libpcre3 \
                    libpcre3-dev \
                    zlib1g \
                    zlib1g-dev \
                    libssl1.1 \
                    libssl-dev \
                    -y && \
    apt-get clean && rm -rf /var/lib/apt/lists/*  #clean all shit we 
                                                #don´t need 
COPY nginx-1.19.2.tar.gz .     #COPY the nginx in to our image
                        # COPY <Source> <destination>
RUN tar -xvf nginx-1.19.2.tar.gz && rm nginx-1.19.2.tar.gz
# run tar -xvf extrahate ter.gz      rm delete the nginx-19.....
RUN cd nginx-1.19.2 && \        
    ./configure \
        --sbin-path=/usr/bin/nginx \        #install Software from 
        --conf-path=/etc/nginx/nginx.conf \ #source right way 
        --error-log-path=/var/log/nginx/error.log \ 
        --http-log-path=/var/log/nginx/access.log \
        --with-pcre \
        --pid-path=/var/run/nginx.pid \
        --with-http_ssl_module && \
    make && make install

RUN rm -rf /nginx-1.19.2  # after ending installation we delete     
                            nginx......

CMD ["nginx", "-g", "daemon off;"] 

# we can build an Image with 
-- docker image build --tag custom-nginx:built .

# Now we are modifying our template to make our script multifunctional. 
# For this, we need the ARG function, which allows us to create variables 
# versionirig in the past 
# to have the option to get the source from the internet we can use ADD for example 

FROM ubuntu:focal

RUN apt-get update && \
    apt-get install build-essential\ 
                    libpcre3 \
                    libpcre3-dev \
                    zlib1g \
                    zlib1g-dev \
                    libssl1.1 \
                    libssl-dev \
                    -y && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
# for nginx-1.19.2 we use the ARG Filename
# for tar.gz we use the ARG EXTEMSION
ARG FILENAME="nginx-1.19.2"
ARG EXTENSION="tar.gz"
# With the ADD comand we can get somting from the World wide web 
ADD https://nginx.org/download/${FILENAME}.${EXTENSION} .

RUN tar -xvf ${FILENAME}.${EXTENSION} && rm ${FILENAME}.${EXTENSION}

RUN cd ${FILENAME} && \
    ./configure \
        --sbin-path=/usr/bin/nginx \
        --conf-path=/etc/nginx/nginx.conf \
        --error-log-path=/var/log/nginx/error.log \
        --http-log-path=/var/log/nginx/access.log \
        --with-pcre \
        --pid-path=/var/run/nginx.pid \
        --with-http_ssl_module && \
    make && make install

RUN rm -rf /${FILENAME}

CMD ["nginx", "-g", "daemon off;"]

# at next we update our Image an build it again and tag it with V"
-- docker image build --tag custom-nginx:built-v2 .
-- docker container run --rm --detach --name custom-nginx-built --publish 8080:80 custom-nginx:built-v2

