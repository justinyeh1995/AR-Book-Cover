# AR-Book-Cover

## Instructions

1. Important Links

- [Video link 1](https://vanderbilt.box.com/s/7skn7t2kggvezo33ktxgngyikg89nof9)
- [Video link 2](https://vanderbilt.box.com/s/1vrfedrdquhbq3aj8depgnn63bkd8tja)
- [Project3.zip on Box](https://vanderbilt.box.com/s/e0keiclfjln3k6f09yecotbqab7oiak3)

2. Download Project3.zip
```bash
Use the link above
```
or
```
git clone git@github.com:justinyeh1995/AR-Book-Cover.git
```

3. Upzip Project3.zip
```bash
upzip Project3.zip
```

4. Add it to Unity Project from Unity Hub

5. Add SampleScene from Assests/Scene to Project

6. Click Play

---

## Discussions

The Virtual Button did not track the onButtonPressed well enough. As we can see in video link 2, it lost track of the gestures several times.
  

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
