# Earthquake-prediction-
combination of Image processing and seismic precursors

Earthquake Magnitude Prediction Based on Combination of Seismic Indicators and Interferometry Technique 
Mahsa Tadrisinoor 
Department of Electrical and computer Enginnering 
Shiraz University
Shiraz,Iran
m.tadrisinoor@shirazu.ac.ir
 
Mehran Yazdi
Department of Electrical and computer Enginnering
Shiraz University
Shiraz,Iran
M.yazdi@shirazu.ac.ir
 
Mahmoud Sharzehi
Iranian Space Research 
Centre
Mechanics Research Institute
Shiraz, Iran
Msharzeh@yahoo.com 
 
 
 
Abstract- In this paper, a new technique for earthquake magnitude prediction has been presented to forecast the following 14 days. The algorithm uses both ground deformation map and seismic data as indicators to predict the possibility of forthcoming earthquakes. Since there is no application of interferometry technique in earthquake prediction and also no empirical relationship between seismic indicators and earth displacement caused by earthquakes. In this study, eight components as indicators have been derived by using magnitude and occurrence time of the historical earthquakes which occurred in Kermanshah province which is one of the major earthquake-prone area in Iran. Later on, the ground deformation was calculated by using Interferometry technique of Synthetic Aperture Radar (SAR) images from there. These data were applied to Recurrent Neural Network (RNN), in order to achieve the highest prediction accuracy and obtaining the appropriate results. The proposed technique has been evaluated by using three different statistical measures: False Alarm Ratio (FAR), the Probability of Detection and R-score. In general, the recurrent neural network model yields the highest forecasting accuracies with a high degree of certainty by combining seismic indicators and earth displacement derived by interferometry technique. The proposed method was trained and tested using data from Kermanshah province.
Keywords—earthquake prediction, Synthetic Aperture Radar, Interferometry technique

	Introduction 
An earthquake is the most destructive natural hazard and it is difficult to predict exactly where and when it will happen. It can broadly cause significant damages to buildings and other infrastructures[1]. Studies related to earthquake prediction range from theoretical geophysics, to mutations and biology, to statistical, mathematical, and computational modeling of earthquake parameter data recorded in historical catalogs of seismic regions [2]. In 12th November 2017, an earthquake of Mw 7.3 hit the border region between Iran and Iraq. The epicenter (34.90°N, 45.95°E) is located at 30 km south of Halabjah city in Iraq and 51 km north of Sarpol Zahab. The strongest aftershock of around 4.7 and more than 350 aftershocks with Mw>2.5 were recorded [3]. It left more than 12000 people injured and damaged some 30000 houses and this disaster led to the conviction that an innovative approach in earthquake prediction should be tested.
       Previous studies predicted earthquake occurrence based on Seismicity indicators and they are utilized as training dataset to the neural networks, while in this proposed method the Recurrent neural network ,yielding the best accuracy in preceding studies, have an extra input which is allocated to ground displacement. The goal of this research is to introduce a new method combining SAR Interferometery technique and mathematically calculated seismic indicators from temporal distribution of historic recorded seismic events, as inputs of neural networks to achieve more accurate magnitude prediction of future earthquakes.
       An interesting method in assessment of the ground deformation has been Synthetic Aperture Radar interferometry (InSAR) and Sentinel-1 SAR images have been used in this research from 2017 to 2019.  It is necessary to first introduce the indicators and give a sufficient understanding of each parameter. First we give a brief review of previous studies with the purpose of earthquake forecasting, the next section deals with the land deformation measurement based on the Interferometric Synthetic Aperture Radar (InSAR) in certain days before and after the mentioned earthquake. The proceeding stages devoted to neural network which is shown and tested to evaluate the earthquake forecasting. 

	Literature Review
Earthquake prediction models have no capability to exactly state time, location and magnitude of the future occurrences. In [4] the Gutenberg-Richter mathematical model has shown that earthquake magnitudes are related to occurrence frequency. One study has been carried out in 2007, showing that occurring earthquakes always follow poison's distribution time independent model [5]. Another earthquake prediction model ,presenting the earthquake occurrence of magnitude greater than 5, has been proposed based on extraction of irregular features of earthquake occurring [6], examining the strain accumulated between the plates [7] and past earthquakes extrapolation for forecasting future seismic events [8].
       By the advances which have been made in the field of Artificial Neural Networks and Machine learning, there exists remarkable influence in predicting or classification purposes especially in seismic events. Observing changes taking place in the concentration of radon gas by using Back-Propagation Neural Network [9], predicting earthquakes using past earthquake magnitude data as input of Radial Basis Function [10] , training Probabilistic Neural Network with 8 seismic indicators [2] are some attempts to predict earthquakes. In 2013, scientists presented different seismic indicators [11] by  studying Bath's and Omori's law [12] aim in finding the relationship between earthquake occurrence and seismic parameters. The application of fuzzy logic has been combined with neural networks (named ANFIS model ) by Zamani in 2013[13].

	Seismic Indicators
In this section, eight seismicity indicators are selected based on conclusions which were drawn by earthquake forecasting experiments to evaluate the seismic potential of a region [14]. The seismic catalogue was provided by Iranian Seismological Center (IRSC).Time span, mean magnitude and seismic energy square root as well as temporal distribution of earthquake magnitude are completely independent, while three of indicators- the slope of Gutenberg-Richter curve (b-value), the mean square deviation summation and the magnitude deficit (∆M) are based on temporal magnitude distributions. The remaining two indicators (c-value and µ-value) are based on the characteristic temporal earthquake magnitude distribution. The values of the precursors with ground deformation are inputs of RNN in section IV. 
       As it is shown in Equation (1), the first seismic indicator is T representing the time span covering n number of seismic events with magnitude greater than threshold.
T = tn – t1                                                                                    (1)
       Where tn shows nth occurrence time and t1 is the time of first event. Time span states the foreshocks' frequency depending on the magnitude threshold [14]. The second seismic indicator is known as mean magnitude of the last n number of seismic activity and is defined as (see Eq. (2)):
Mmean=∑_n^(i=1)▒M_i                                                                         (2)
       The foreshocks' magnitude mean is also crucial in some regions regarding the hypothesis of accelerated release the magnitude of earthquake increases immediately before the main shock.
       As regards the seismic quiescence phenomenon, gradual release of seismic energy can be observed through occurring earthquakes with low magnitudes but if this process stops, it can result in major earthquakes. The third precursor is related to seismic energy released over time T, is given in the following equation (3):
dE1/2 = ∑▒〖E^(1/2)/T〗                                                                   (3)
       Where the seismic energy (E) can be calculated from the Eq. (4).
E= 10(11.8+1.5 M) ergs                                                                (4)
       B-value is another seismic indicator which is based on Gutenberg-Richter inverse power law. B is the curve-slope between magnitude and logarithm of frequency of the earthquake which is defined as:
log_10⁡N=a-bM                                                                  (5)
       Equation (5) declares that the N number of earthquakes of magnitude equal to or greater than M decreases exponentially with M. In other word, the difference between small and large seismic events and the level of seismicity in the area can be determined by b-value and a-value respectively. Both parameters can be computed using the following relationships (see Eq. (6) and Eq. (7)):
b=  (n∑▒〖(M_i  log⁡〖N_i 〗 )-∑▒〖M_i ∑▒log⁡〖N_i 〗 〗〗)/(〖(∑▒M_i )〗^2-n∑▒M_i^2 )                                                   (6)
a=  (∑▒〖(log_10⁡〖N_i 〗+bM_i)〗)⁄n                                                   (7)
       In equation (7) N_i is the number of earthquakes with magnitude M> M_i occurring within the time span of T and  M_i is magnitude of the ith event and n is the summation of seismic event number. 
       Mean square deviation is the third parameter based on Gutenberg-Richter inverse power-law which is calculated by using equation (8). 
η =(∑▒〖(log_10⁡〖N_i 〗-(a-bM_i))〗^2 )⁄((n-1))                               (8)
       The higher appropriateness of the Gutenberg-Richter power law in estimating the magnitude and frequency occurrence of the earthquake distribution can be found by lower value of η. Magnitude deficit is based on temporal magnitude distribution showing the difference between the largest expected and the largest occurred magnitude.
       Mmax,expected is the maximum expected event based on the parameters of the Gutenberg-Richter inverse power law which an be found in Eq. (9).
Mmax,expected=a/b                                                                      (9)
       The gap observed between typical seismic events is called mean time given in equation (10).
µ =(∑▒(t_(i characteristic) ) )⁄n_characteristic                                    (10)
       As an illustration, earthquakes with magnitude between 4 and 4.5 are classified into one group and considered as characteristic magnitude. Variation coefficient is the aperiodicity of the c-value and known as a seismic precursor calculated from equation (11) which shows the deviation from mean time. High value for c indicates that the calculated and the observed time average are so different.
c=  (standard deviation of the observed times )⁄μ   (11)

	Interferometric Indicators
Microwave remote sensing techniques such as Synthetic Aperture Radar interferometry (InSAR), are much more interesting tools, In comparison with geodetic techniques. These approaches are capable of generating maps with sub-centimeters accuracies by deriving surface deformation. [15] The dataset information is summarized in Table 1. Figure 1 presents the area of interest and the whole frame of the image has been processed in creating interferogram. All scenes were provided by the European Space Agency (ESA). The Interferometric Wide-Swath(IW mode) which are the main TOPS mode of the Sentinel-1 satellites has three subswaths, with wide swath of around 250 km on the ground, includes incidence angles within the range of 30° and 45°. The pixel size of each IW mode is in the range of 20m×5m (azimuth versus range direction) [16]. The multi-temporal interferometry (MTI) of Sentinel-1 imagery (descending track) was performed with GMTSAR software. 
 
Fig .1 Area of interest is shown in bold rectangle
Table 1 SAR Data information used in this research 
Sensor	Sentinel-1
	Number of scene	Time interval	Sensor's pass	SAR mode
	112	2015-2019	Descending	IWa
Interferometeric Wide Swath

	Datasets
Before combining interferometry technique with seismic indicators, we divided the 5-year period into 120 14-days groups and also widened the time period into 10 years and again we had 120 30-days groups. We concluded that trained network with 5 years data of two-week time period had more accurate results in magnitude prediction. In Table 2, the results of comparing two time period were summarized. 
Table 2 Comparing the reliability of 14-days and 30-day time period selection in earthquake magnitude prediction  
	POD	FAR	R-score
14-days	0.714	0.2	0.514
30-days	0.75	0.36	0.39

In comparison with [2], based on the analysis of the eight seismicity indicators, 14-days period leads to more accurate verification parameters which will be described in following sections. False alarm ratio shows that although 30-days selection of time period resulted in more probability of detection, it can be ignorable when it comes to greater FAR. Moreover, as R-score is better reliability assessment metrics and equally represents correct and false prediction, the more R-score our method demonstrates, the more reliable datasets it will be ,so 14-day time period was found more appropriate for prediction.
 A nine-element vector of combination of seismicity and interferometry indicators is corresponded to every 14-day time period from February 2015 to December 2019 is classified into two  groups, depends on the predicted group, if the maximum magnitude is predicted to be greater than the predefined magnitude (it was considered 5 Richter in this study), it is classified into first group which relates to occurred earthquakes and in the cases that no earthquake was occurred greater than 5 Richter, it belongs to second group. In order to modify the results, the depth of earthquake was added to input vector and a better result with higher accuracy was achieved. 
The satellite works in 5.405 GH which has four mode of imaging (IW, EW, SM, WV). In this research 112 raw Sentinel-1 SAR acquisition of descending track were processed for the period 2015 to 2019. The period covers the 2017 devastating earthquake occurred in Kermanshah. Initially we focused on the raw data to Single Look Complex (SLC) images, using Digital Elevation Model (DEM) GMTSAR software to process interferograms and we used the orbital data of the ESA website (https://qc.sentinel1.eo.esa.int/) to gain accurate satellite position. For the estimation and subtraction of topography effect, we used the SRTM DEM [17]. The selection of master and slave images was based on the minimum temporal baseline threshold which was less than 4 month.

	Neural Network Architecture And Operation
Recently ,In [14] the author utilized 8 mathematically calculated parameters known as seismic indicators to examine the capability of 3 neural networks, a recurrent neural network (RNN), a radial basis function (RBF) neural network and a feed-forward Levenberg-Marquardt back-propagation (LMBP) neural network in order to predict the seismic event of the largest magnitude in the forthcoming month [18]. In this research, the description and schematic of recurrent neural network have been presented as shown in Table 3 because it led to the best prediction accuracy in the previous researches.
Table 3 Recurrent Neural Network Architecture 
Architecture	Training parameters
Number of layers	1(8 input)
1 recurrent    (1 input)	Learning rule

Output	Levenberg-marquardt
0: non-occurrence
1: occurrence
Number of neurons	5 
5(recurrent)	Learning rate
MSE	0.01

0.01
Activation function	Tan-sigmoid	Iteration	10000

6.1 Recurrent Neural Network (RNN) 
In Figure 3 the structure of a recurrent neural network has been shown. In each iteration, output of the network is went through the layer of recurrent and then for achieving the predicted output, the summation is fed to the transfer function. Output is computed as defined in equation (12).
O_pi=∑_(i=1)^n▒〖f(s_i.w_j+O_p(i-1) .w_r)〗                                      (12)
       O_piis the only element output which represents that the earthquake of magnitude>= threshold will happen in the ith time period (1) or will not happen (0), s_i is the vector of input consisting of the seismicity indicators and interferometry data for the ith time period, w_jand w_r are the weight vectors connecting the nodes in the input layer to the nodes in the jth hidden layer and the nodes of the recurrent layer to the output node. Also, n is the number of hidden layers and f is the activation function of the network.
       Training the recurrent neural network is performed by minimizing the mean square error between the predicted and the observed outputs using Levenberg-Marquardt training algorithm [19]. The applicable structure of RNN used in this research can be found in Fig. 2.  
 
Fig .2 Structure of RNN in order to predict magnitude of the following major earthquakes[19]
6.2 Modification of RNN
The recurrent neural network is first modeled with an input layer of eight nodes, one hidden layer and one node in recurrent layer as shown in Figure 3. Once dimension of input vector corresponding to a given month was increased to 9×1 rather than 8, considering the displacement in prediction accuracy. The aim of this study is to verify the qualification of forecasting by modifying the seismic indicators.
  Fig .3 Structure of Recurrent Neural Network with different training data (a) seismic indicators (b) combination of seismic indicators and earth displacement derived by ineterferometry method.
       As the previous architectures, the network output of (1) represents the occurrence and (0) non-occurrence of the threshold magnitude or greater during the following time period.  For converging the value of Mean Square Error (MSE) and the number of training iteration should be limited to 0.001 and 1000, respectively. 
6.3 Prediction Verification
Three different statistical measures were used to evaluate the prediction accuracy: the probability of detection (POD), false alarm ratio (FAR), frequency bias (FB), and R scores. These three evaluating criteria are calculated by the following equations. (See Eq. (13), Eq. (14) and Eq. (15))
POD=N_pc/(N_pc+N_ni )                                                                     (13)
FAR=N_pi/(N_nc+N_pi )                                                                      (14)
FB=(N_pc+N_pi)/(N_pc+N_ni )                                                                       (15)
       Where N_pc is the number of time periods algorithm correctly predict an actual occurred earthquake, N_pi (predicted incorrect) is the number of time periods a predicted seismic activity did not happen in actual. Regarding the output value of 0, N_ncis the number of time periods during which the algorithm correctly predict the non-occurrence of the earthquake and N_ni is the number of time periods algorithm falsely did not predict the actual seismic events. All these parameters are summarized in Table 4.
Table 4 Variables used for calculation of POD, FAR and FB
                predicted                           
observed
	Yes	no
yes	N_pc	N_pi
no	N_ni	N_nc

	Prediction Results
In order to evaluate the earthquake prediction accuracy, we compared the output of network with the actual occurred earthquake by counting the number of false and correct predictions. Occurred earthquakes in the following month were classified into two groups. earthquakes and conclude the quality by computing POD, FAR and FB in each group.
7.1 Moderate earthquake Prediction (Magnitude greater than 5)
In testing period corresponding to Kermanshah province in Iran, there exists 28 time periods which have earthquake with magnitude greater than 5. The recurrent neural network which was trained with seismic indicators failed to predict the occurrence of 13 earthquakes. The value of POD in this case was 0.535 and FAR in the range of 0.206. In contrast, by training the network with both seismic indicator and earth displacement derived by interferometry technique, 16 events were predicted and we achieved better values in POD and FAR, equal to 0.571 and 0.1764 respectively, indicating that most of the predictions were completely correct. Furthermore, R-score in RNN trained with seismic indicator and earth displacement demonstrated greater value in comparison with the network trained with seismic indicators-(0.329 and 0.3946)
        In order to evaluate the effect of depth in prediction accuracy of moderate earthquakes, we added depth in to input vector and surprisingly there was a slight improvement in result in comparison with combination of seismic indicators and interferometry data. 
In Table 5, computed values of number of false and correct prediction were summarized. 
Table 5 The value of Npc, Npi, Nnc and Nni with different input datasets during the 5 years
	Npc	Npi	Nnc	Nni
Seismic indicators	15	13	50	20
Seismic indicators+ Earth displacement	16	12	56	14
Seismic indicator+ Earth displacement+ Depth	17	11	59	11

	Real time evaluation
Apart from prediction accuracy obtained by Recurrent Neural Network trained by the combination of seismic and interferometric data, time complexity is also a key aspect of the proposed approach which should be taken into consideration. To evaluate the processing speed of the algorithm, the research is conducted in the medium system with the operating system of windows 8, 4GB RAM, Intel i3 in MATLAB (R2018b). The average time cost of different data sets have been provided in Table 5. It can be seen that the average time cost is less than 3 seconds with different input datasets, which is short enough to meet most real time requirements.
Table 5 Prediction average time of the proposed datasets
Input vector	Average time cost(s)
Seismic indicators	2.954
Seismic and interferometry indicators	2.876
Seismic and interferometry indicators and depth	2.889

	Final Coments
Earthquake indicators have been studied for many years and generally they are considered as unpredictable parameters and also predicting or modeling earthquake is a complex problem. A large number of scientists have tried to understand the exact relationship between indicators and probability of occurrence but it cannot be completely understood.
       In this study a new approach has been tried in order to utilize interferometry technique in the area of earthquake prediction. A Recurrent Neural Network was presented which tend to show the least false alarm compared with other neural network such as BPNN or RBF with different architectures.
       The results show that earthquake displacement can provide useful information on the earthquake analysis. Finally, a nine-dimensional input vector including seismic and interferometry indicators can be considered a reliable databases within the framework of earthquake prediction system.  
Acknowledgment
It is with great pleasure that the authors convey their sincere thanks to all those who helped me to complete this work. Also thanks to Scihub Copernicus website (https://scihub.copernicus.eu/dhus/#/home) for providing the Sentinel images. Also the author gratefully acknowledge the provision of some of the figures for illustrating various aspects and application of SAR interferometry and neural network architecture.
References
	Tamkuan, N. and M. Nagai, SENTINEL-1A ANALYSIS FOR DAMAGE ASSESSMENT: A CASE STUDY OF KUMAMOTO EARTHQUAKE IN 2016. MATTER: International Journal of Science and Technology, 2019. 5(1).
	Adeli, H. and A. Panakkat, A probabilistic neural network for earthquake magnitude prediction. Neural networks, 2009. 22(7): p. 1018-1024.I. S. Jacobs and C. P. Bean, “Fine particles, thin films and exchange anisotropy,” in Magnetism, vol. III, G. T. Rado and H. Suhl, Eds. New York: Academic, 1963, pp. 271–350.
	Raucoules, D., et al., Surface displacement of the Mw 7 Machaze earthquake (Mozambique): Complementary use of multiband InSAR and radar amplitude image correlation with elastic modelling. Remote Sensing of Environment, 2010. 114(10): p. 2211-2218.
	Dahmen, K., D. Ertaş, and Y. Ben-Zion, Gutenberg-Richter and characteristic earthquake behavior in simple mean-field models of heterogeneous faults. Physical Review E, 1998. 58(2): p. 1494.
	Petersen, M.D., et al., Time-independent and time-dependent seismic hazard assessment for the State of California: Uniform California Earthquake Rupture Forecast Model 1.0. Seismological Research Letters, 2007. 78(1): p. 99-109.
	Kagan, Y.Y., D.D. Jackson, and Y. Rong, A testable five-year forecast of moderate and large earthquakes in southern California based on smoothed seismicity. Seismological Research Letters, 2007. 78(1): p. 94-98.
	Shen, Z.-K., D.D. Jackson, and Y.Y. Kagan, Implications of geodetic strain rate for future earthquakes, with a five-year forecast of M5 earthquakes in southern California. Seismological Research Letters, 2007. 78(1): p. 116-120.
	Ebel, J.E., et al., Non-Poissonian earthquake clustering and the hidden Markov model as bases for earthquake forecasting in California. Seismological Research Letters, 2007. 78(1): p. 57-65.
	Negarestani, A., et al., Layered neural networks based analysis of radon concentration and environmental parameters in earthquake prediction. Journal of environmental radioactivity, 2002. 62(3): p. 225-233.
	Liu, Y., et al. Earthquake prediction by RBF neural network ensemble. in International Symposium on Neural Networks. 2004. Springer.
	Morales-Esteban, A., F. Martínez-Álvarez, and J. Reyes, Earthquake prediction in seismogenic areas of the Iberian Peninsula based on computational intelligence. Tectonophysics, 2013. 593: p. 121-134.
	Båth, M., Lateral inhomogeneities of the upper mantle. Tectonophysics, 1965. 2(6): p. 483-514.
	Utsu, T. and Y. Ogata, The centenary of the Omori formula for a decay law of aftershock activity. Journal of Physics of the Earth, 1995. 43(1): p. 1-33.
	Zamani, A., M.R. Sorbi, and A.A. Safavi, Application of neural network and ANFIS model for earthquake occurrence in Iran. Earth Science Informatics, 2013. 6(2): p. 71-85.
	Panakkat, A. and H. Adeli, Neural network models for earthquake magnitude prediction using multiple seismicity indicators. International journal of neural systems, 2007. 17(01): p. 13-33.
	Kampes, B.M., R.F. Hanssen, and Z. Perski. Radar interferometry with public domain tools. in Proceedings of FRINGE. 2003.
	Floyd, M.A., et al., Spatial variations in fault friction related to lithology from rupture and afterslip of the 2014 South Napa, California, earthquake. Geophysical Research Letters, 2016. 43(13): p. 6808-6816.
	Farr, T.G. and M. Kobrick, Shuttle Radar Topography Mission produces a wealth of data. Eos, Transactions American Geophysical Union, 2000. 81(48): p. 583-585.
	Schmidt, D.A. and R. Bürgmann, Time‐dependent land uplift and subsidence in the Santa Clara valley, California, from a large interferometric synthetic aperture radar data set. Journal of Geophysical Research: Solid Earth, 2003. 108(B9).
	Panakkat, A. and H. Adeli, Recurrent neural network for approximate earthquake time and location prediction using multiple seismicity indicators. Computer‐Aided Civil and Infrastructure Engineering, 2009. 24(4): p. 280-292.
	Hagan, M., H. Demuth, and M. Beale, Neural network design, PWS Publishing company. Boston, USA, 1995.
	Shirazu55
 



1.	Tamkuan, N. and M. Nagai, SENTINEL-1A ANALYSIS FOR DAMAGE ASSESSMENT: A CASE STUDY OF KUMAMOTO EARTHQUAKE IN 2016. MATTER: International Journal of Science and Technology, 2019. 5(1).
2.	Adeli, H. and A. Panakkat, A probabilistic neural network for earthquake magnitude prediction. Neural networks, 2009. 22(7): p. 1018-1024.
3.	Raucoules, D., et al., Surface displacement of the Mw 7 Machaze earthquake (Mozambique): Complementary use of multiband InSAR and radar amplitude image correlation with elastic modelling. Remote Sensing of Environment, 2010. 114(10): p. 2211-2218.
4.	Dahmen, K., D. Ertaş, and Y. Ben-Zion, Gutenberg-Richter and characteristic earthquake behavior in simple mean-field models of heterogeneous faults. Physical Review E, 1998. 58(2): p. 1494.
5.	Petersen, M.D., et al., Time-independent and time-dependent seismic hazard assessment for the State of California: Uniform California Earthquake Rupture Forecast Model 1.0. Seismological Research Letters, 2007. 78(1): p. 99-109.
6.	Kagan, Y.Y., D.D. Jackson, and Y. Rong, A testable five-year forecast of moderate and large earthquakes in southern California based on smoothed seismicity. Seismological Research Letters, 2007. 78(1): p. 94-98.
7.	Shen, Z.-K., D.D. Jackson, and Y.Y. Kagan, Implications of geodetic strain rate for future earthquakes, with a five-year forecast of M5 earthquakes in southern California. Seismological Research Letters, 2007. 78(1): p. 116-120.
8.	Ebel, J.E., et al., Non-Poissonian earthquake clustering and the hidden Markov model as bases for earthquake forecasting in California. Seismological Research Letters, 2007. 78(1): p. 57-65.
9.	Negarestani, A., et al., Layered neural networks based analysis of radon concentration and environmental parameters in earthquake prediction. Journal of environmental radioactivity, 2002. 62(3): p. 225-233.
10.	Liu, Y., et al. Earthquake prediction by RBF neural network ensemble. in International Symposium on Neural Networks. 2004. Springer.
11.	Morales-Esteban, A., F. Martínez-Álvarez, and J. Reyes, Earthquake prediction in seismogenic areas of the Iberian Peninsula based on computational intelligence. Tectonophysics, 2013. 593: p. 121-134.
12.	Utsu, T. and Y. Ogata, The centenary of the Omori formula for a decay law of aftershock activity. Journal of Physics of the Earth, 1995. 43(1): p. 1-33.
13.	Zamani, A., M.R. Sorbi, and A.A. Safavi, Application of neural network and ANFIS model for earthquake occurrence in Iran. Earth Science Informatics, 2013. 6(2): p. 71-85.
14.	Panakkat, A. and H. Adeli, Neural network models for earthquake magnitude prediction using multiple seismicity indicators. International journal of neural systems, 2007. 17(01): p. 13-33.
15.	Kampes, B.M., R.F. Hanssen, and Z. Perski. Radar interferometry with public domain tools. in Proceedings of FRINGE. 2003.
16.	Floyd, M.A., et al., Spatial variations in fault friction related to lithology from rupture and afterslip of the 2014 South Napa, California, earthquake. Geophysical Research Letters, 2016. 43(13): p. 6808-6816.
17.	Farr, T.G. and M. Kobrick, Shuttle Radar Topography Mission produces a wealth of data. Eos, Transactions American Geophysical Union, 2000. 81(48): p. 583-585.
18.	Panakkat, A. and H. Adeli, Recurrent neural network for approximate earthquake time and location prediction using multiple seismicity indicators. Computer‐Aided Civil and Infrastructure Engineering, 2009. 24(4): p. 280-292.
19.	Hagan, M., H. Demuth, and M. Beale, Neural network design, PWS Publishing company. Boston, USA, 1995.

