# BYOST (Build Your Own Spectral Template)

Using Principal Component analysis (PCA) and Gaussian Process Regression (GPR) to build a spectral template based on two conditions (such as time and light-curve-shape parameter). 
This work is initially developped to construct the NIR spectral template of type Ia supernovae using the data obtained by CSP-II, see our [publication](https://arxiv.org/abs/2211.05998) for details. 

But it does NOT need to be limited to spectroscopic data, you can use this for other modeling purposes as long as the dataset and attached conditions show correlations (all value need to be finite).  The major process is:
- Apply PCA on the dataset to reduce the dimension to a small subspace
- Moeling the subspace (PC projection values) dependence on the given conditons using GPR 
- Inverse PCA transformation using the predicted PC from GPR given disired condition


## Installation
```
pip install BYOST
```

## Quick guide

#### NIR spectral template for type Ia supernova (from Lu2023)

If you would like to use the new NIR spectral template for type Ia supernova, please download the data products (NIR_Ia_template_buildingblocks.tar) of Lu2023 from the [CSP data website](https://csp.obs.carnegiescience.edu/data).

After you have downloaded buildingblock file "NIR_Ia_template_buildingblocks.pkl", you can run the following in python to get the template with given input phase and sBV values. 

```
import BYOST

df_buildingblock = pd.read_pickle('NIR_Ia_template_buildingblocks.pkl')

phase = 10  # input phase of the template spectra
sBV = 0.9  # input sBV of the template spectra
template = BYOST.template.get_template(df_buildingblock,phase,sBV,return_template_error=True)

## set return_template_error=False if you don't need template_flux_err,it takes some time to compute
## template[0] is the template wavelength, and template[1] is the template flux
## template[2] is the template flux error if return_template_error=True 
```

#### General useage of the this packge
For general useage of the this packge, please see the quick guide that is provided in the notebook [BYOST_quick_guide.ipynb](https://github.com/DeerWhale/BYOST/blob/main/BYOST_quick_guide.ipynb).

## Cites
If you used this package for your research work, please kindly cite [our paper](https://arxiv.org/abs/2211.05998), much appriciated! :)
