# AR-Book-Cover

## Instructions

### 1. Important Links

- Recoreded With Natural Sun Light: [Video link 1](https://vanderbilt.box.com/s/7skn7t2kggvezo33ktxgngyikg89nof9)
- Recoreded W/O Nature Light: [Video link 2](https://vanderbilt.box.com/s/1vrfedrdquhbq3aj8depgnn63bkd8tja)
- Recoreded With Artificial Bright Light: [Video link 3](https://vanderbilt.box.com/s/folklol2v2zhbdre5h0je1iu1ekpnvzp)

### 2. Download Project3.zip

Download the zip file via [Project3.zip on Box](https://vanderbilt.box.com/s/e0keiclfjln3k6f09yecotbqab7oiak3)

or
```
git clone git@github.com:justinyeh1995/AR-Book-Cover.git
```

### 3. Upzip Project3.zip
```bash
upzip Project3.zip
```

### 4. Add it to Unity Project from Unity Hub

<img width="247" alt="Screenshot 2024-02-20 at 10 40 22 PM" src="https://github.com/justinyeh1995/AR-Book-Cover/assets/42970023/8bf2b2b5-6bc4-4276-8647-e343f798f504">

### 5. Add SampleScene from Assests/Scene to Project

![Screenshot 2024-02-20 at 10 42 11 PM](https://github.com/justinyeh1995/AR-Book-Cover/assets/42970023/866b5bbb-e9bc-4e8f-a96e-3527c13aaf9f) 

![Screenshot 2024-02-20 at 10 41 41 PM](https://github.com/justinyeh1995/AR-Book-Cover/assets/42970023/056a0fec-f1a7-4679-8a3b-987dbca16036) 

### 6. Click Play

![Screenshot 2024-02-20 at 10 44 14 PM](https://github.com/justinyeh1995/AR-Book-Cover/assets/42970023/34bd147a-8236-4059-abbd-ead5623da0ee)


---

## Discussions

### Results
The Virtual Button did not track the onButtonPressed well enough in the first two video. As we can see in video link 1 & 2, it lost track of the gestures several times.
However, in video 3, a bright LED light was used, and it made the tracking better as we can see the improved responsiveness.

### Implementing the behavior of the virtual button
The code below implements the logic of toggling texts between detailed descriptions and reviews. It can also be found in `VBTN.cs`. The logic is quite straightforward.
1. Set up objects' states in `Start`, and make sure `OnButtonPressed` and `OnButtonReleased` are registered on the virtual button.
2. The main toggling logic is in `OnButtonPressed` where a boolean flag is used to control the visibility of two types of texts
3. `OnButtonReleased` logs out dummy information, which asserts this function is triggered.  

```csharp
// Tutorial: https://www.youtube.com/watch?v=Ckw4RKKVE3k
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Vuforia;

public class VBTN : MonoBehaviour
{
    public GameObject cube;
    public GameObject detailText;
    public GameObject reviewText;
    public VirtualButtonBehaviour vrb;
    private bool isShowingDetails = true;

    // Start is called before the first frame update
    void Start()
    {
        vrb.GetComponent<VirtualButtonBehaviour>();

        vrb.RegisterOnButtonPressed(OnButtonPressed);
        vrb.RegisterOnButtonReleased(OnButtonReleased);
        
        cube.SetActive(true);
        detailText.SetActive(true);
        reviewText.SetActive(false);
        // detailsText = GameObject.Find("DetailsTextName");
        // reviewText = GameObject.Find("ReviewTextName");
    }


    public void OnButtonPressed(VirtualButtonBehaviour vrb)
    {
        Debug.Log("OnButtonPressed: " + vrb.VirtualButtonName);

        if (isShowingDetails) 
        {
            detailText.SetActive(false);
            reviewText.SetActive(true);
            isShowingDetails = false;
        }
        else
        {
            detailText.SetActive(true);
            reviewText.SetActive(false);
            isShowingDetails = true;
        }
    }


    public void OnButtonReleased(VirtualButtonBehaviour vrb)
    {
        Debug.Log("OnButtonReleased: " + vrb.VirtualButtonName);
    }

}
```
