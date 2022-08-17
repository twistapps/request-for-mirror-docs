
[Mirror](https://mirror-networking.com/) is an Open Source Networking library for Unity.

If you want to support all of the `Mirror's` **NetworkBehaviour** features in your modules,
we got you!

Simply derive from `NetworkModule` instead of `Module` for the seampless Mirror - Modula integration:

{% highlight C# %}
public class Shooting : NetworkModule
{
    [SyncVar] public bool isShooting;

    public override TypeList RequiredOtherModules { get; } = new TypeList()
        .Add(typeof(Turret));
        
    private RigidBody _rb;

    public override void Awake()
    {
        base.Awake();
        _rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        if (isLocalPlayer)
        {
            var shootingButtonPressed = Input.GetMouseButton(0);
            if (!isShooting && shootingButtonPressed)
                CmdSetShooting(true);
            else if (isShooting && !shootingButtonPressed) CmdSetShooting(false);
        }

        if (isServer) HandleShooting();
    }

    [Command]
    public void CmdSetShooting(bool shooting)
    {
        isShooting = shooting;
    }

    [Server]
    public void HandleShooting()
    {
        if (!isShooting) return;
        SpawnBullet( ... );
    }
}
{% endhighlight %}
    
All the attributes etc will work as if you were just using NetworkBehaviour.

All the Modula's features are still supported tho! Such as ModuleUpdate()

#Important Notices
While migrating to `NetworkModule` from `NetworkBehaviour`, don't forget to override Awake()
and put base.Awake() to use [optimization features](optimizations.md).