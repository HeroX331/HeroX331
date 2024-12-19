Here is a more advanced script that includes the features you mentioned:
```
// Auto Fish Script

using UnityEngine;

public class AutoFish : MonoBehaviour
{
  public float speed = 5f;
  public float turnSpeed = 5f;
  public float castDistance = 10f;
  public float castSpeed = 10f;
  public float reelSpeed = 5f;

  private Rigidbody rb;
  private bool isCasting = false;
  private bool isReeling = false;

  void Start()
  {
    rb = GetComponent<Rigidbody>();
  }

  void Update()
  {
    // Auto walk on water
    if (transform.position.y >= 0.5f)
    {
      rb.velocity = new Vector3(rb.velocity.x, 0f, rb.velocity.z);
    }

    // Auto shake (simulate fishing rod shaking)
    transform.Rotate(Vector3.up, Mathf.Sin(Time.time * 5f) * 10f);

    // Auto fishing
    if (!isCasting && !isReeling)
    {
      // Cast line
      isCasting = true;
      GetComponent<Rigidbody>().AddForce(transform.forward * castSpeed, ForceMode.Impulse);
      Invoke("ReelIn", castDistance / castSpeed);
    }

    // Auto reel in
    if (isReeling)
    {
      rb.velocity = -transform.forward * reelSpeed;
    }
  }

  void ReelIn()
  {
    isCasting = false;
    isReeling = true;
    Invoke("StopReeling", castDistance / reelSpeed);
  }

  void StopReeling()
  {
    isReeling = false;
  }
}
```
This script includes the following features:

- Auto walk on water: The fish will automatically walk on the water's surface.
- Auto shake: The fish will simulate a fishing rod shaking motion.
- Auto fishing: The fish will automatically cast its line and reel it back in.
- Auto throw cast: The fish will automatically throw its cast.

Note that this script uses Unity's physics engine to simulate the fishing mechanics, so you may need to adjust the values of the public variables to get the desired behavior.
