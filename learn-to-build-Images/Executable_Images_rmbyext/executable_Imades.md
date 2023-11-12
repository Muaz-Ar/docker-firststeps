# we will create an executable_Images in this lection 
# firs: what is our Task
# we will create an executable Image an we get the source from gitHub
# it will be create by Python 

# second: What did we need to do this
# 1. at the image we need Python, we need a copy of the package what pip installs and we must install git becaus the repo comes from ther 

# lets start 

FROM python:3-alpine

WORKDIR /zone

RUN apk add --no-cache git && \
    pip install git+https://github.com/fhsinchy/rmbyext.git#egg=rmbyext && \
    apk del git

ENTRYPOINT [ "rmbyext" ]

# The WORKDIR instruction sets the default working directory to /zone here. The name of the working directory is completely random here. I found zone to be a fitting name, you may use anything you want.

# Finally on line 9, the ENTRYPOINT instruction sets the rmbyext script as the entry-point for this image.