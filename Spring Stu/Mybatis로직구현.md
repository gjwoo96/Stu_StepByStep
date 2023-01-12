> Service
- @service 어노테이션
```
public int writeComment(CommentDto comment);
```

> ServiceImpl
- Service Implements 
- @Autowired(객체주입) DAO
```
@Autowired
    private CommentDao commentDao;

     @Override
    public int writeComment(CommentDto comment) {
        return commentDao.writeComment(comment);
    }
```

> DAO
- @Repositroy
- @Autowired(객체주입) SqlSessionTemplate 
```
    @Autowired
    protected SqlSessionTemplate sqlSession;
    
    private static String namespace = "com.edu.comment.dao.CommentDao";
    
    @Override
    public int writeComment(CommentDto comment) {
        return sqlSession.insert(namespace+".writeComment", comment);
    }
```

참고: (https://bigfat.tistory.com/95)
____


