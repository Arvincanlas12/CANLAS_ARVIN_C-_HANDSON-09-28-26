// Codes



using UninityEngine;

public class GridMovement: MonoBehaviour
{
    public float tileSize = 1.0f;
    public float moveSpeed = 10f;
    
    private Vector3 targetPosition;
    private bool is Moving = False;

    void Start()
    {
        targetPosition = SnapToGrid(Transform.position);
        transform.position = targetPosition;
        
    }
    void Update()
    {
        if (!isMoving)
        {
            HandleInput();
        }
        else
        {
        if (Vector3.Distance(transform.position, targetPosition)<0.0001f
            {
            transform.position = targePosition;
            isMoving = false;
        }
    }
}
void HandleInput()
            {
                Vector3 direction = Vector.zero;
                if (Input.GetKeyDown(KeyCode. W)) direction = Vector3.up;
                else if (Input.GetKeyDown(KeyCode. S)) direction = Vector3.down;
                else if (Input.GetKeyDown(KeyCode. A)) direction = Vector3.left;
                else if(Input.GetKeyDown(KeyCode. D)) direction = Vector3.right;
                if(direction ! = Vector3.zero)
                {
                    targetPosition = transform.position + direction * tileSize; 
                    isMoving = true;
            }
        }
            Vector3 SnapToGrid(Vector3 pos)
            {
                return new Vector3(
                    Mathf.Round(pos.x / tileSize) * tileSize,
                    Mathf.Round(pos.y / tileSize) * tileSize,
                    pos.z
                );               
                )
        }
}

using UnityEngine;
            
public class FreeMovement : MonoBehaviour
            
            public float moveSpeed = 5f;

            void Update()
            {
            float horizontal = Input.GetAxis("Horizontal");
            float vertical = Input.GetAxis("Vertical");

            Vector3 direction = new Vector3(horizontal, vertical, 0f);
            if(direction.magnitude>1f)
            {
                direction.Normalize();
            }
            transform.position += direction * moveSpeed * Time.deltaTime;
            
        }
}    

using UnityEngine;
[requireComponent(typepof(Rigidbody2D))]
            
public class PhysicsMovement : MonoBehaviour
{
    public float moveForce = 10f;
    public float jumpForce = 7f;
    public float maxSpeed = 6f;

    private float Rigidbody2D rb;
    private bool isGrounded = false;
    
    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }
    void Update()
    {
    if(Input.GetKeyDown(KeyCode.Space) && isGrounded)
    {
        rb.AddForce(Vector2.up * jumpForce, ForceMode2D.Impulse);
    }
    }
    void FixedUpdate()
{
    float horizontal = InputGetAxis("Horizontal");
    rb.Addforce(new Vector2(horizontal * moveForce, 0f));
    if(Mathf.Abs(rb.Velocity.x)>maxSpeed)
    {
    rb.velocity = newVector2(Mathf.Sign(rb.vekocity.x)) * maxSpeed, rb.velocity.y 
    }
}
void OnCollisionEnter2D(Collision2D collision)
    {
    if(collision.gameObject.CompareTag("Ground"))
        {
        isGrounded = true;
        }
    }
    void OnCollisionExit2D(Collision 2D collision)
    {
        if(collision.gameObject.CompareTag("Grounded"))
        {
        isGrounded = false; 
        }
    }
}
