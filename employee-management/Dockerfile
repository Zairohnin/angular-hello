FROM depauna/nvm:latest as preparedbuilder
ADD package.json employee-management/
ADD package-lock.json employee-management/
ADD install.sh employee-management/install.sh
WORKDIR /employee-management
RUN ./install.sh

FROM preparedbuilder as builder
ADD . /employee-management/
WORKDIR /employee-management/
ENV APIURL="https://kubernetes-elb-depauna-127443764.eu-west-1.elb.amazonaws.com/user29backend"
RUN ./build.sh user29frontend

FROM depauna/apache:latest
COPY --from=builder /employee-management/dist/employee-management /var/www/html/user29frontend
CMD httpd -X
