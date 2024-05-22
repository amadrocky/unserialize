# unserialize
Populate object by unserialization process

```php
use Doctrine\ORM\EntityManagerInterface;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\Serializer\Normalizer\AbstractNormalizer;
use Symfony\Component\Serializer\SerializerInterface;

class Create {
  public function __construct(
    private SerializerInterface $serializer,
    private EntityManagerInterface $entityManager
  ) {
  }
  
  private function populateObject(Request $request): void
  {
    $object = new Object();
  
    $this->serializer->deserialize(
        json_encode($request->request->all()),
        Object::class,
        'json',
        [AbstractNormalizer::OBJECT_TO_POPULATE => $object]
    );

    $this->entityManager->persist($object);
    $this->entityManager->flush();
  }
}
```
