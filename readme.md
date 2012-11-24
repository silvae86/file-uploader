# "Multi"-Fine Uploader 3.0 (Released November 16) #

Modified to enable uploading a single file to many endpoints, calling the onComplete handler for every request that is concluded. 

The data from each endpoint is supplied to the onComplete handler for different actions.

An example usage, where a file is sent to two endpoints (note the new endpoint array) and the JSON responses are used to change two different divs in my html:

```javascript
                    var uploader = new qq.FineUploader({
                      // Pass the HTML element here
                      element: document.getElementById('uploader'),
                      request: {
                        endpoint: ["file_query/plain_results", "file_query/propagated_results"],
                        forceMultipart: true
                      },
                      
                      text: {
                        uploadButton: '<i class="icon-upload icon-white"></i> Select or drop a file here'
                        },
                        
                      template: '<div class="qq-uploader span12">' +
                                  '<pre class="qq-upload-drop-area span12"><span>{dragZoneText}</span></pre>' +
                                  '<div class="qq-upload-button btn btn-success" style="width: auto;">{uploadButtonText}</div>' +
                                    '<ul class="qq-upload-list" style="margin-top: 10px; text-align: center;"></ul>' +
                                  '</div>',
                              
                      classes: {
                            success: 'alert alert-success',
                            fail: 'alert alert-error'
                        },  
                        
                      callbacks: {
                          onComplete: function(id, fileName, responseJSON)
                            {
                                if(responseJSON.query_type == "simple")
                                {
                                    buildTableFromFileQueryResponse(responseJSON, fileName, "#search-results-normal", "simple-results-table", "#main");
                                }
                                else if (responseJSON.query_type == "propagated")
                                {
                                    buildTableFromFileQueryResponse(responseJSON, fileName, "#search-results-propagated", "propagated-results-table", "#main");    
                                }    
                            }
                      }, 
                      debug: true
                    });
```

# Based on Fine Uploader 3.0 (Released November 16) #