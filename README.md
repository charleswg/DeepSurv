# DeepSurv

DeepSurv implements a deep learning generalization of the Cox proportional hazards model using Theano and Lasagne. 

DeepSurv has an advantage over traditional Cox regression because it does not require an *a priori* selection of covariates, but learns them adaptively. 

DeepSurv can be used in numerous survival analysis applications. One medical application is provided: recommend_treatment, which provides treatment recommendations for a set of patient observations. 

For more details, see full paper [Deep Survival: A Deep Cox Proportional Hazards Network](http://arxiv.org/abs/1606.00931).

## Installation:

### Dependencies

Theano, Lasagne, lifelines, matplotlib (for visualization) and all of their respective dependencies. 

### Installing

You can install *DeepSurv* using

	pip install deepsurv
	pip install --upgrade https://github.com/Theano/Theano/archive/master.zip
	pip install --upgrade https://github.com/Lasagne/Lasagne/archive/master.zip
	pip install matplotlib


from the command line.

#### Dependencies

DeepSurv has been succesfully installed and tested on macOS Sierra 10.12.1 with the follow versions of Python packages:

        'theano==0.10.0.dev1',
        'lasagne==0.2.dev1',
        'lifelines==0.11.1',

### Running the tests

After installing, you can optionally run the test suite with

	py.test

from the command line while in the module main directory.

## Training a Network

Training DeepSurv can be done in a few lines. 
First, all you need to do is prepare the datasets to have the following keys:

	{ 
		'x': (n,d) observations (dtype = float32), 
	 	't': (n) event times (dtype = float32),
	 	'e': (n) event indicators (dtype = int32)
	}

Then prepare a dictionary of hyper-parameters. And it takes only two lines to train a network:

	network = deepsurv.DeepSurv(**hyperparams)
	log = network.train(train_data, valid_data, n_epochs=500)

You can then evaluate its success on testing data:

	network.get_concordance_index(**test_data)
	>> 0.62269622730138632

If you have matplotlib installed, you can visualize the training and validation curves after training the network:

	deepsurv.plot_log(log)
