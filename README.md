# AR-Book-Cover

[video link](https://vanderbilt.box.com/s/7skn7t2kggvezo33ktxgngyikg89nof9)

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