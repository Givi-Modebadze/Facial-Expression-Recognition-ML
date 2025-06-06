# Facial-Expression-Recognition-ML

wandb report link: https://api.wandb.ai/links/gmode-free-university-of-tbilisi-/d6k2qtnn

რეპოზიტორიის სტრუქტურა: 
    
    -- SimpleCNN.ipynb
      ძალიან მარტივი კონვულუციური მოდელი
    
    -- ImprovedCNNv1.ipynb
      გაუმჯობესებული მოდელი
    
    -- BetterCNN.ipynb
      ამ ეტაპისთვის საუკეთესო მოდელი

    -- README.md


SimpleCNN.ipynb არქიტექტურა:

    2 Convolutional ფენა + MaxPooling
    
    2 Fully Connected ფენა
    
    Activation: ReLU
    
    Loss: CrossEntropyLoss
    
    Optimizer: Adam

    Epochs: 10

  მოდელის მიზანი იყო მარტივი ექსპერიმენტის ჩატარება და შესაბამისად Accuracy საკმაოდ დაბალია ~50%, ასევე ვერ ითვისებს კომპლექსურ მონაცემებს ანუ ხდება underfitting.


ImprovedCNNv1.ipynb არქიტეწტურა:

    დამატებულია მეტი Conv ფენა
  
    Batch Normalization ყოველი Conv ფენის შემდეგ
  
    Dropout სრულად დაკავშირებულ ფენებზე
  
    Learning Rate Scheduler დამატებულია
  
    Activation: ReLU

    Epochs: 10

  მოდელის მიზანი იყო კომპლექსურობის გაზრდა და მეათე epoch-ზე Train Acc=0.6750, Val Acc=0.6158 მიაღწია. მცირედი overfitting შესამჩნევია, თუმცა BatchNorm და Dropout აშკარად ეფექტურია. სავარაუდოდ შედეგის ასეთი ზრდა გამოწვეულია უპირველესად კონვოლუციური ფენის დამატებით, თუმცა ნორმალიზაციამ და დროფაუთმაც ითამაშა თავისი როლი.


BetterCNN.ipynb

    3x Conv ბლოკი:
        Conv2D → BatchNorm → LeakyReLU → MaxPooling
        
    2x Fully Connected ბლოკი:
        Linear → BatchNorm → LeakyReLU → Dropout
        
    Output Layer: Linear (num_classes)
    
    Loss: CrossEntropyLoss
    
    Optimizer: Adam
    
    Activation: LeakyReLU
    
    Data Augmentation: HorizontalFlip, Rotation, ResizedCrop
    
    Normalization: Mean=0.5, Std=0.5
    
    Epochs: 30

  შედეგი:
  
      | Epoch | Train Accuracy | Val Accuracy |
      |-------|----------------|--------------|
      | 10    | 58.24%         | 60.71%       |
      | 20    | 68.05%         | **64.19%**   |
      | 30    | ~69%           | **64.82%**   |

  მოდელი აშკარად გაუმჯობესდა. 10 epoch-ზე გამოვლენილი შედეგის გამო, სადაც ვალიდაციაზე უკეთესი შედეგი ჰქონდა ვიდრე ტრეინზე, ცხადი გახდა, რომ მოდელს უფრო დიდი პოტენციალი ჰქონდა. შესაბამისად 30 მდე გავაგრძელებინე ტრენინგი, რამაც ვალიდაცია ~64% მდე აიყვანა. განსხვავებული ჰიპერპარამეტრების მოსინჯვით ალბათ გაცილებით უკეთესი შედეგის დადებაც შეიძლებოდა, თუმცა 30 epoch-ს დაახლოებით 3 საათი დასჭირდა, ამიტომ ვფიქრობ ესეც სავსებით საკმარისია.

  პ.ს. ჩატარებული ექსპერიმენტები დალოგილია wandb-ზე სადაც შეგიძლიათ იხილოთ უფრო დეტალურად თითოეული მოდელის პერფორმანსი.



  
