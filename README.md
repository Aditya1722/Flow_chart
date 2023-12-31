# Flow_chart



**Step 1** - PRESTO

* Use single_pulse_search.py of presto to get a file with ouput example as shown in below -
  |   DM     |  SNR    |  tsamp   | Downsample |
  | -------- | ------- | -------- | ---------- |
  |   40     |   8     |   20     |     2      |
  |   40     |   10    |   25     |     8      |
  |   45     |   12    |   30     |     16     |

* Sort these files on the basis of DM and then combine all these data in a single file.

**Step 2** - SPEGID
 
* convert the output of all the file in a csv format (it only accepts csv ) example   
  **DM,SNR,tsamp,Downsample**  
  40, 8 , 20  ,  2  
  40, 10, 25  ,  8
  
* one more file to create with extension .inf consiting of these information -  
  **object_obs , RA , Dec , central_freq_low_chan , total_bandwidth**  
  G33.79+00.82.N , 18:49:51.1792 , 01:07:02.6874 , 1214.28955078 , 322.6171875
  
* output  of SPEGID will contain information of all the terms mentioned below being the columms -  
  **filename  ,RA	, Dec	, SPEG_rank	,group_rank	, group_peak_DM	, group_max_SNR ,	group_median_SNR ,	merged , sizeU , size	, peak_DM_spacing	, peak_DM	, peak_time , peak_SNR ,	peak_sampling ,	peak_downfact	, min_DM	, max_DM ,	min_time ,	max_time ,	centered_DM ,	center_startDM ,	center_stopDM ,	clipped_SPEG ,	SNR_sym_index ,	DM_sym_index ,	peak_score ,	bright_recur_times ,	recur_times	cluster_number ,	DM_channel_number	, obs_length** 
   
**Step 3** - Need to figure out the threshold for chosing candidate from output of SPEGID and then pass them to make h5 files 

**Step 4** - generating h5 files of selected candidates
* Your is module whose one of the tool is generating hDf file format and then plotting them .  
* The python sript we use is `your_candmaker.py` 
   * `your_candmaker.py` uses one more script `candidat.py` [Here](https://github.com/thepetabyteproject/your/blob/72f2f988521e4095d2a29132ce8f74cbd8d994de/bin/your_candmaker.py")
   * Difficulty in running sigporoc fake generated data . So i replaced the script of  `your_candmaker.py` with the modified `your_candmaker.py` of CHIME pipeliene(CHIPSPIPE) [Here](https://github.com/CHIME-Pulsar-Timing/CHIME-Pulsar_automated_filterbank/blob/main/your_candmaker.py")
   * `your_candmaker.py` requires two things -
     * cand.csv - consisiting information of  
                - file: Filterbank or PSRFITs file containing the data. In case of multiple files, this should contain the name of first file.   
                - snr: Signal to Noise of the candidate.  
                - width: Width of candidate as log2(number of samples).   
                - dm: DM of candidate  
                - label: Label of candidate (can be just set to 0, if not known)  
                - stime: Start time (seconds) of the candidate.  
                - chan_mask_path: Path of the channel mask file.     
                - num_files: Number of files.
      * filterbank file(.fil)  - should provide the path to the directory
  * Syntax -  
            ` your_candmaker.py -c cand.csv -o path/to/output/directory/ `  
  * Output -   
     ![download](https://github.com/Aditya1722/Flow_chart/assets/73752922/5a36c15e-b301-4dfc-9e68-8c7741e6d98f)

    
* **Step 5** - Manual inspection of these plots 
