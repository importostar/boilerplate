---
title: processing_geocode
date: 2020-05-07
---
Example Python program processing_geocode.py

## Modules

* from qgis.processing import alg
* from qgis.core import QgsFeature, QgsGeometry, QgsPoint, QgsField, QgsFeatureSink, QgsNetworkAccessManager, QgsWkbTypes, QgsExpression, QgsExpressionContextUtils, QgsCoordinateReferenceSystem
* from PyQt5.QtCore import QUrl, QVariant
* from PyQt5.QtNetwork import QNetworkRequest
* import json

## Classes

* class NominatimGeocoder():
* class GoogleGeocoder():

## Methods

* def __init__(self):
* def request_uri(self, address):
* def process_response(self, response):
* def __init__(self, api_key):
* def request_uri(self, address):
* def process_response(self, response):
* def geocode(instance, parameters, context, feedback, inputs):

## Code

Example Python PyQt program :

    from qgis.processing import alg
    from qgis.core import QgsFeature, QgsGeometry, QgsPoint, QgsField, QgsFeatureSink, QgsNetworkAccessManager, QgsWkbTypes, QgsExpression, QgsExpressionContextUtils, QgsCoordinateReferenceSystem
    from PyQt5.QtCore import QUrl, QVariant
    from PyQt5.QtNetwork import QNetworkRequest
    import json
    
    class NominatimGeocoder():
        """A geocoder for nominatim"""
        
        def __init__(self):
            pass
            
        def request_uri(self, address):
            return 'https://nominatim.openstreetmap.org/search?format=json&q={address}'.format(address=address)
    
        def process_response(self, response):
            res = []
            for rec in response['results']:
                res.append((rec['display_name'], QgsPoint(float(rec['lon']), float(rec['lat']))))
            return res
    
    class GoogleGeocoder():
        """a geocoder for google. Needs an API key"""
        def __init__(self, api_key):
            self.api_key=api_key
            
        def request_uri(self, address):
            return 'https://maps.googleapis.com/maps/api/geocode/json?address={address}&key={key}'.format(address=address, key=self.api_key)
    
        def process_response(self, response):
            res = []
            for rec in response['results']:
                res.append((rec['formatted_address'], QgsPoint(float(rec['geometry']['location']['lng']), float(rec['geometry']['location']['lat']))))
            return res
    
    @alg(name="geocode", label=alg.tr("GeoCode"), group="examplescripts", group_label=alg.tr("GeoCode"))
    @alg.input(type=alg.SOURCE, name="INPUT", label="Adress layer", default="asdf")
    @alg.input(type=alg.EXPRESSION, name="EXPRESSION", label="Address expression", parentLayerParameterName="INPUT", default=" 'Bnei Brak ' || \"Field3\" || ' ' ||  \"Field1\" ")
    @alg.input(type=alg.ENUM, name="SERVICE", label="Service", options=['Google', 'Nominatim'], default="Google")
    @alg.input(type=alg.STRING, name="API_KEY", label="Google API key", default="AIzaSyDFyl_TY4QMBEmthl2m2DKCUmv1hL0yqF8")
    @alg.input(type=alg.SINK, name="OUTPUT", label="Output layer")
    def geocode(instance, parameters, context, feedback, inputs):
        """
        Geocode locations. Addresses in, points out.
        May produce multiple points for an address if ambiguous.
        """
        source = instance.parameterAsSource(parameters, "INPUT", context)
        exp = instance.parameterAsExpression(parameters, "EXPRESSION", context)
        service = instance.parameterAsExpression(parameters, "SERVICE", context)
        api_key = instance.parameterAsExpression(parameters, "API_KEY", context)
     
        fields = source.fields()
        fields.append(QgsField('DisplayName', QVariant.String))
        (sink, dest_id) = instance.parameterAsSink(
            parameters, "OUTPUT", context,
            fields, QgsWkbTypes.Point, QgsCoordinateReferenceSystem(4326))
     
        total = 100.0 / source.featureCount() if source.featureCount() else 0
        features = source.getFeatures()
        exp_context = context.expressionContext()
        exp_context.appendScope(source.createExpressionContextScope())
        expression = QgsExpression(exp)
        expression.prepare(exp_context)
        
        if service == 'Nominatim':
            geocoder = NominatimGeocoder(api_key)
        else:
            geocoder = GoogleGeocoder(api_key)
    
        for current, feature in enumerate(features):
            if feedback.isCanceled():
                break
            exp_context.setFeature(feature)
            address = expression.evaluate(exp_context)
            
            request = QNetworkRequest(QUrl(geocoder.request_uri(address)))
            reply = QgsNetworkAccessManager.blockingGet(request)
            response = json.loads(str(reply.content().data(), encoding='utf-8'))    
            
            out_feature = QgsFeature(fields)
            for field in source.fields():
                out_feature[field.name()] = feature[field.name()]
                
            for result in geocoder.process_response(response):
                out_feature.setGeometry(QgsGeometry(result[1]))
                out_feature['DisplayName'] = result[0]
                sink.addFeature(out_feature, QgsFeatureSink.FastInsert)
                
            feedback.setProgress(int(current * total))
     
        return {"OUTPUT": dest_id}
        

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
