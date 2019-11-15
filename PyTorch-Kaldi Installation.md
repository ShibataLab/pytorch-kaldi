# Fork and Maintain changes from original repository
[Source](https://digitaldrummerj.me/git-syncing-fork-with-original-repo/)

Fork original repository in Github.

Clone forked repository.

	git clone git@github.com:ShibataLab/pytorch-kaldi.git
	cd pytorch-kaldi

Setup original repository as upstream to get changes from original repository.

	git remote -v
	# origin	git@github.com:ShibataLab/pytorch-kaldi.git (fetch)
	# origin	git@github.com:ShibataLab/pytorch-kaldi.git (push)

	git remote add upstream https://github.com/mravanelli/pytorch-kaldi.git
	git remote -v
	# origin	git@github.com:ShibataLab/pytorch-kaldi.git (fetch)
	# origin	git@github.com:ShibataLab/pytorch-kaldi.git (push)
	# upstream	https://github.com/mravanelli/pytorch-kaldi.git (fetch)
	# upstream	https://github.com/mravanelli/pytorch-kaldi.git (push)

To get changes from original repository:

	git fetch upstream

Then, make sure you are on 'master' branch:
	
	git checkout master

Merge changes from upstream/master to local master branch

	git merge upstream/master

# Create PyEnv VirtualEnv for PyTorch-Kaldi

	pyenv install 3.7.4
	pyenv virtualenv 3.7.4 pytorch-kaldi
	pyenv local pytorch-kaldi

# Prerequisites

1. Make sure Kaldi is installed. Please check [forked Kaldi repository](https://github.com/ShibataLab/kaldi/blob/mac/Kaldi%20Installation.md) for details on how to install Kaldi.

	1. Patch system environment variable PATH to include Kaldi
	
		**Note: Make sure to supply the correct KALDI_ROOT**

			tee -a ~/.zshrc << END
			export KALDI_ROOT=/home/noel-desktop/Projects/kaldi
			# export IRSTLM=\$KALDI_ROOT/tools/irstlm
			# export LIBLBFGS=\$KALDI_ROOT/tools/liblbfgs-1.10
			# export LD_LIBRARY_PATH=\${LD_LIBRARY_PATH:-}:\${LIBLBFGS}/lib/.libs
			# export SRILM=\$KALDI_ROOT/tools/srilm
			PATH=\$PATH:\$KALDI_ROOT/tools/openfst
			PATH=\$PATH:\$KALDI_ROOT/src/featbin
			PATH=\$PATH:\$KALDI_ROOT/src/gmmbin
			PATH=\$PATH:\$KALDI_ROOT/src/bin
			PATH=\$PATH:\$KALDI_ROOT/src/nnetbin
			PATH=\$PATH:\$KALDI_ROOT/tools/python
			# PATH=\$PATH:\$KALDI_ROOT/tools/kaldi_lm
			# PATH=\$PATH:\$IRSTLM/bin
			# PATH=\$PATH:\$SRILM/bin:\$SRILM/bin/i686-m64
			export PATH
			END

	2. Close terminal and test if PATH has been properly patched.

		``copy-feats`` should show something like this...

			copy-feats 
			
			Copy features [and possibly change format]
			Usage: copy-feats [options] <feature-rspecifier> <feature-wspecifier>

		``hmm-info`` should show something like this...

			hmm-info 

			Write to standard output various properties of HMM-based transition model
			asasf

2. Make sure [PyTorch](http://pytorch.org/) is installed.
	
	1. Install [PyTorch](http://pytorch.org/).

		For Mac:

			pip3 install torch torchvision

		For Ubuntu:

			pip3 install torch==1.3.1+cpu torchvision==0.4.2+cpu -f https://download.pytorch.org/whl/torch_stable.html

	2. Check if PyTorch has been installed.

		**Note: There should be no errors when running this command.**

			python -c "import torch"

# Install needed packages

	pip install -r requirements.txt