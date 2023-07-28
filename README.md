## README ##

### Program file ###
There are 2 program files
(1) Aidea_train.ipynb   :  Use for training process
(2) Aidea_test.ipynb    :  Use for testing process

### Build Environment ###
<Step.1> : Please download all "hfd5" file and "ckpt" file from following connection 
            https://drive.google.com/drive/folders/1WIwse2gGgs5t0CkjYdztatfQFpvR0WMf?usp=sharing
<Step.2> : Move into your google drive and make the file named after "Aidea_data"
<Step.3> : Move all "hfd5 file" into your builded file "Aidea_data"

### Block ###
請打開Google Colab:

(1)對於 Aidea_train.ipynb : 
    (a) 先掛載自己的雲端硬碟, 且確認好自己雲端硬碟建立好的資料夾 "Aidea_data" 路徑為 '/content/drive/MyDrive/Aidea_data'
    (b) Parameter settings : 
        num_class : 預設為14, 代表14個類別
        batch_size : 每一epoch中每一批次更新參數時所輸入的影像張數, 預設為16
        n_epochs : 總共訓練的回合數, 預設為15
        model_selection : 選擇要訓練的model , 1代表Efficient Net b3 ; 2代表Efficient Net b4 ; 3代表Efficient Net b6 , 預設為1
        _exp_name : 每次訓練完儲存參數, 模型狀態, 優化器狀態的檔案名稱 (即checkpoint名稱)
        retrain : 因為Google Colab運行24小時就會自斷斷線,因此要重Checkpoint訓練時(載入Checkpoint Path)就開啟成True , 預設為False
    (c) 然後可以對每一模塊開始run , 包括 Mount Google Drive, Check GPU Type, Import Package, Parameters settings, Random Seed Settings, 
        Copy hdf5(image format) file from Google Drive, Data augmentation, Dataset Preparing, Cope with data imbalance with WeightedRandomSampler, 
        Function, Training的所有模塊進行run
        #label = 0 -> banana
        #label = 1 -> bareland
        #label = 2 -> carrot
        #label = 3 -> corn
        #label = 4 -> dragonfruit
        #label = 5 -> garlic
        #label = 6 -> guava
        #label = 7 -> peanut
        #label = 8 -> pineapple
        #label = 9 -> pumpkin
        #label = 10 -> rice
        #label = 11 -> soybean
        #label = 12 -> sugarcane
        #label = 13 -> tomato

(2)對於Aidea_test.ipynb :
    (a) 先掛載自己的雲端硬碟, 且確認好自己雲端硬碟建立好的資料夾 "Aidea_data" 路徑為 '/content/drive/MyDrive/Aidea_data'
    (b) Parameter settings : 
        [i]_exp_name_model_2, _exp_name_model_3, _exp_name_model_4是我原本自己訓練各個model的參數檔(ckpt), 這邊可以根據自己訓練好的模型所儲存的參數名稱來設定,
        比如說我原本儲存的參數名稱為 _exp_name = "sample_EffNetb3" , 你就會在自己雲端硬碟的Aidea_data下看到自己sample_EffNetb3_best.ckpt,然後可以例如改寫
        _exp_name_model_2 = "sample_EffNetb3" ,那麼在model_2就會載入這個參數檔
        [ii]這邊我原本有訓練五個模型 model_1, model_2, model_3, model_4, model_5 ; 這邊我只取model_2, model_3, model_4這樣3個model做Ensemble效果不錯
        [iii] Setting the number of ensemble model : weight number , 因為三個模型做Ensemble,所以這邊weight_num就設定為3
        [iv]  Setting the TTA weight : alpha, 這邊主要是做Test time augmentation, 我建立10組train augmentation,但用七組就夠了 , 這邊alpha預設為0.965 , 
              TTA_w預設為7(代表七組augmentation)
        ### 三個我的訓練參數load路徑
        ##### For EffNet b3 model_2: "/content/drive/MyDrive/Aidea_data/sample_kk_Effb3_imbalance_best.ckpt"
        ##### For EffNet b4 model_3: "/content/drive/MyDrive/Aidea_data/sample_3_Eff_b4_lrsche_imbalance_imbalancee_best.ckpt"
        ##### For EffNet b6 model_4: "/content/drive/MyDrive/Aidea_data/sample_once_kk_Effb6_imbalance_best.ckpt"
    (c) 然後可以對每一模塊開始run , 包括 Mount Google Drive, Check GPU Type, Parameters settings, Copy the file from google drive into local destination, Import Package,
        Environment Settings, TTA Data augmentation, Test Dataset Preparing, TTA : for various train data augmentation, Test dataloader, Evaluate : TTA+Ensemble,
        Make Predictions的所有模塊進行run
        #label = 0 -> banana
        #label = 1 -> bareland
        #label = 2 -> carrot
        #label = 3 -> corn
        #label = 4 -> dragonfruit
        #label = 5 -> garlic
        #label = 6 -> guava
        #label = 7 -> peanut
        #label = 8 -> pineapple
        #label = 9 -> pumpkin
        #label = 10 -> rice
        #label = 11 -> soybean
        #label = 12 -> sugarcane
        #label = 13 -> tomato
    (d) 在最後模塊Make Predictions : 製作出Submission_TEAM_645.csv檔,請在自己路徑'/content/drive/MyDrive/Aidea_data'下看有沒有輸出成功, 並可下載下來上傳答案
