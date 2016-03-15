

    import graphlab

    A newer version of GraphLab Create (v1.8) is available! Your current version is v1.7.1.
    
    You can use pip to upgrade the graphlab-create package. For more information see https://dato.com/products/create/upgrade.


#Load a common image analysis dataset


    image_train = graphlab.SFrame('data/image_train_data/')
    image_text = graphlab.SFrame('data/image_test_data/')

    [INFO] [1;32m1453385939 : INFO:     (initialize_globals_from_environment:282): Setting configuration variable GRAPHLAB_FILEIO_ALTERNATIVE_SSL_CERT_FILE to /Users/zhaoxu/.graphlab/anaconda/lib/python2.7/site-packages/certifi/cacert.pem
    [0m[1;32m1453385939 : INFO:     (initialize_globals_from_environment:282): Setting configuration variable GRAPHLAB_FILEIO_ALTERNATIVE_SSL_CERT_DIR to 
    [0mThis non-commercial license of GraphLab Create is assigned to brainstudiosg@gmail.com and will expire on December 18, 2016. For commercial licensing options, visit https://dato.com/buy/.
    
    [INFO] Start server at: ipc:///tmp/graphlab_server-17069 - Server binary: /Users/zhaoxu/.graphlab/anaconda/lib/python2.7/site-packages/graphlab/unity_server - Server log: /tmp/graphlab_server_1453385939.log
    [INFO] GraphLab Server Version: 1.7.1


#Exploring the image data


    graphlab.canvas.set_target('ipynb')


    image_train['image'].show()



#Train a classifier on the raw image pixels


    raw_pixel_model = graphlab.logistic_classifier.create(image_train,target='label',
                                                  features=['image_array'],max_iterations=100)

    PROGRESS: Creating a validation set from 5 percent of training data. This may take a while.
              You can set ``validation_set=None`` to disable validation tracking.
    
    PROGRESS: Logistic regression:
    PROGRESS: --------------------------------------------------------
    PROGRESS: Number of examples          : 1908
    PROGRESS: Number of classes           : 4
    PROGRESS: Number of feature columns   : 1
    PROGRESS: Number of unpacked features : 3072
    PROGRESS: Number of coefficients    : 9219
    PROGRESS: Starting L-BFGS
    PROGRESS: --------------------------------------------------------
    PROGRESS: +-----------+----------+-----------+--------------+-------------------+---------------------+
    PROGRESS: | Iteration | Passes   | Step size | Elapsed Time | Training-accuracy | Validation-accuracy |
    PROGRESS: +-----------+----------+-----------+--------------+-------------------+---------------------+
    PROGRESS: | 1         | 6        | 0.000019  | 2.066475     | 0.347484          | 0.360825            |
    PROGRESS: | 2         | 8        | 1.000000  | 2.492082     | 0.393606          | 0.402062            |
    PROGRESS: | 3         | 9        | 1.000000  | 2.739901     | 0.410377          | 0.381443            |
    PROGRESS: | 4         | 10       | 1.000000  | 3.004010     | 0.440252          | 0.402062            |
    PROGRESS: | 5         | 11       | 1.000000  | 3.265790     | 0.448113          | 0.402062            |
    PROGRESS: | 6         | 12       | 1.000000  | 3.545488     | 0.475367          | 0.432990            |
    PROGRESS: | 10        | 16       | 1.000000  | 4.579703     | 0.514675          | 0.546392            |
    PROGRESS: | 11        | 17       | 1.000000  | 4.833208     | 0.519392          | 0.515464            |
    PROGRESS: | 15        | 22       | 1.000000  | 6.096025     | 0.566562          | 0.515464            |
    PROGRESS: | 20        | 27       | 1.000000  | 7.409058     | 0.585430          | 0.597938            |
    PROGRESS: | 25        | 32       | 1.000000  | 8.727234     | 0.593291          | 0.577320            |
    PROGRESS: | 30        | 37       | 1.000000  | 10.052903    | 0.600105          | 0.577320            |
    PROGRESS: | 35        | 42       | 1.000000  | 11.360485    | 0.610587          | 0.556701            |
    PROGRESS: | 40        | 47       | 1.000000  | 12.662120    | 0.633124          | 0.577320            |
    PROGRESS: | 45        | 52       | 1.000000  | 13.959475    | 0.639413          | 0.556701            |
    PROGRESS: | 50        | 57       | 1.000000  | 15.289174    | 0.651468          | 0.587629            |
    PROGRESS: | 51        | 58       | 1.000000  | 15.540393    | 0.649895          | 0.577320            |
    PROGRESS: | 55        | 62       | 1.000000  | 16.573123    | 0.653040          | 0.567010            |
    PROGRESS: | 60        | 67       | 1.000000  | 17.863250    | 0.668239          | 0.556701            |
    PROGRESS: | 65        | 73       | 1.000000  | 19.325882    | 0.676625          | 0.556701            |
    PROGRESS: | 70        | 78       | 1.000000  | 20.648318    | 0.685535          | 0.546392            |
    PROGRESS: | 75        | 84       | 1.000000  | 22.144750    | 0.684486          | 0.525773            |
    PROGRESS: | 80        | 90       | 1.000000  | 23.674538    | 0.694969          | 0.577320            |
    PROGRESS: | 85        | 96       | 1.000000  | 25.198242    | 0.708071          | 0.567010            |
    PROGRESS: | 90        | 101      | 1.000000  | 26.488550    | 0.704927          | 0.525773            |
    PROGRESS: | 95        | 107      | 1.000000  | 27.951263    | 0.716981          | 0.556701            |
    PROGRESS: | 100       | 113      | 1.000000  | 29.442449    | 0.719078          | 0.494845            |
    PROGRESS: +-----------+----------+-----------+--------------+-------------------+---------------------+
    PROGRESS: TERMINATED: Iteration limit reached.
    PROGRESS: This model may not be optimal. To improve it, consider increasing `max_iterations`.


#Make a prediction with the simple model based on raw pixels


    image_text[0:3]['image'].show()




    
