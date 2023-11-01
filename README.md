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
  DM,SNR,tsamp,Downsample  
  40, 8 , 20  ,  2  
  40, 10, 25  ,  8
  
* one more file to create with extension .inf consiting of these information -  
  object_obs , RA , Dec , central_freq_low_chan , total_bandwidth  
  G33.79+00.82.N , 18:49:51.1792 , 01:07:02.6874 , 1214.28955078 , 322.6171875
  
* output  of SPEGID will contain information of all the terms mentioned below being the columms -  
  filename  ,RA	, Dec	, SPEG_rank	,group_rank	, group_peak_DM	, group_max_SNR ,	group_median_SNR ,	merged , sizeU , size	, peak_DM_spacing	, peak_DM	, peak_time , peak_SNR ,	peak_sampling ,	peak_downfact	, min_DM	, max_DM ,	min_time ,	max_time ,	centered_DM ,	center_startDM ,	center_stopDM ,	clipped_SPEG ,	SNR_sym_index ,	DM_sym_index ,	peak_score ,	bright_recur_times ,	recur_times	cluster_number ,	DM_channel_number	, obs_length 
   
**Step 3** - Need to figure out the threshold to chosing the candidate to pass make h5 files 

**Step 4** - generating h5 files of selected candidates
* Your is module whose one of the tool is generating h5 files and then plotting them .  
* The python sript we use is `your_candmaker.py` 
 
**Step 5** - Manual inspection of these plots 
