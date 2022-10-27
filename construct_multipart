    def construct_multipart(self, data, files):
        multi_part = QtNetwork.QHttpMultiPart(QtNetwork.QHttpMultiPart.ContentType.FormDataType)
        for key, value in data.items():
            post_part = QtNetwork.QHttpPart()
            post_part.setHeader(QtNetwork.QNetworkRequest.KnownHeaders.ContentDispositionHeader,
                                "form-data; name=\"{}\"".format(key))
            post_part.setBody(str(value).encode())
            multi_part.append(post_part)
        for field, filepath in files.items():
            file = QtCore.QFile(filepath)
            if not file.open(QtCore.QIODevice.OpenModeFlag.ReadOnly):
                break
            post_part = QtNetwork.QHttpPart()
            post_part.setHeader(QtNetwork.QNetworkRequest.KnownHeaders.ContentDispositionHeader,
                                "form-data; name=\"{}\"; filename=\"{}\"".format(field, file.fileName()))
            post_part.setBodyDevice(file)
            file.setParent(multi_part)
            multi_part.append(post_part)
        return multi_part
