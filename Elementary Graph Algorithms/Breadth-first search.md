//pseudocode
```
BFS(g,S)
  for each vertex u in G.V-{s}：
    u.color=White 
    u.d=inf
    u.pi=NULL
  s.color=Gray
  s.d=0
  s.pi=NULL
  Q=0
  enqueue(Q,s)
  while Q!=0：
    u=dequeue(Q)
    for each v in G.Adj[u]:
    if v.color==White：
      v.color=Gray 
      v.d=u.d+1
      v.pi=u
      enqueue(Q,v)
    u.color=Black
```

      
      
//print
```
Print_path(G,s,v):
  if v==s:
    print v
  elif v.pi==NIL:
    print "no path from s to v"
  else:
    Print_path(G,s,v.pi)
    print v
```    
