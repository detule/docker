FROM python:3.8-alpine
RUN \
 apk add --no-cache --virtual .build-deps gcc musl-dev libffi-dev openssl-dev && \
 pip install mycli==1.22.2 && \
 apk --purge del .build-deps
RUN mkdir /out
VOLUME [ "/out" ]
ENTRYPOINT ["mycli"]