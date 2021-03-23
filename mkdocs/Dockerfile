FROM alpine
RUN apk add --no-cache                                                            \
      build-base curl wget make git                                               \
      python3 python3-dev py3-pip                                                 
     
## Install the mkdocs system
RUN pip3 install mkdocs \
      mkdocs-material mkdocs-nature \
      && rm -rf "$HOME/.cache"

## Define our Entrypoint script
#ENTRYPOINT ["/cmds"]

## The default command for the entrypoint script, show the help message
CMD ["help"]
