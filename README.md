# demo
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class Finish : MonoBehaviour
{
    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.gameObject.name == "nazi")
        {
            SceneManager.LoadScene("Menu");
        }
    }
}
--------------------------------------------------

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerControl : MonoBehaviour
{
    public float speed = 3;
    public float jump = 10;

    private Rigidbody2D rb2D;
    void Start()
    {
        rb2D = GetComponent< Rigidbody2D >();
    }//Start

    void Update()
    {
        float move = Input.GetAxis("Horizontal");
        rb2D.velocity = new Vector2( move * speed , rb2D.velocity.y );
        if ( Input.GetKeyDown(KeyCode.Space) )
        {
            rb2D.AddForce( new Vector2( 0 , jump ) ,ForceMode2D.Impulse );
        }
    
     }// Update
}//PlayerControl
--------------------------------------------------------------------------------

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ShootPoint : MonoBehaviour
{
    public GameObject target;
    public Transform shootPoint;
    public Rigidbody2D bullet;
        
    void Update()
       {
                if ( Input.GetMouseButtonDown( 0 ) )
            {
                Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
                Debug.DrawRay(ray.origin, ray.direction * 20, Color.yellow, 5);
                
                RaycastHit2D hit = Physics2D.GetRayIntersection(ray, Mathf.Infinity);

        if (hit.collider != null)
            {
                target.transform.position = new Vector2(hit.point.x, hit.point.y);
                Debug.Log(" Hit point : " + hit.point);
 
                Vector2 projectileV = CalculateProjectile(shootPoint.position, hit.point, 1);
                Rigidbody2D spawnBullet = Instantiate(bullet, shootPoint.position, Quaternion.identity);
                spawnBullet.velocity = projectileV;
            
            }//hit

            }//GetMouseButtonDown
      
       }//Update

       Vector2 CalculateProjectile(Vector2 origin, Vector2 targetPoint, float time)
       {
        Vector2 distance = targetPoint - origin;
        
        float velocityX = distance.x / time;
        float velocityY = distance.y / time + 0.5f * Mathf.Abs(Physics2D.gravity.y) * time;

        Vector2 projecttileVelocity = new Vector2(velocityX, velocityY);

        return projecttileVelocity;

        }
    

}//ShootPoint
-------------------------------------------------------------------------------------

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class StartButton : MonoBehaviour
{
    private void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.collider.name == "StartButton")
        {
            SceneManager.LoadScene("GamePlay");
        }
 
    }

}
---------------------------------------------------







