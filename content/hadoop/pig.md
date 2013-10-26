Apache Pig
==========

Create New Tuple and Bag
------------------------

    #!java
    import org.apache.pig.data.Tuple;
    import org.apache.pig.data.TupleFactory;
    import org.apache.pig.data.DataBag;
    import org.apache.pig.data.BagFactory; 

Create Factory

    #!java
    TupleFactory tupleFactory   = TupleFactory.getInstance();
    BagFactory bagFactory       = BagFactory.getInstance(); 

Use Factory to create Tuple and Bag

    #!java
    Tuple tuple     = tupleFactory.newTuple();
    DataBag dataBag = bagFactory.newDefaultBag(); 

Notes: Tuple is an interface, we cannot create Tuple using ``Tuple tuple = new Tuple();`` Instead we create a TupleFactory first.

    #!java
    public abstract class TupleFactory {
        private static TupleFactory gSelf = null;
        
        public static TupleFactory getInstance();

        ...
    } 

Quote from API documentation: "This class is abstract so that users can override the tuple factory if they desire to provide their own that returns their implementation of a tuple. If the property pig.data.tuple.factory.name is set to a class name and pig.data.tuple.factory.jar is set to a URL pointing to a jar that contains the above named class, then ``getInstance()`` will create a an instance of the named class using the indicated jar. Otherwise, it will create an instance of DefaultTupleFactory."
``getInstance()`` is used to "get a reference to the singleton factory." Where singleton means there will be only one gSelf. If it is not null, the function will return gSelf, instead of generating a new factory.

Output Schema the Easier Way
----------------------------

Instead of building schema using Schema and FieldSchema from ground up, we could use ``Utils.getSchemaFromString()`` to generate schema directly from a string. 

    #!java
    import org.apache.pig.impl.util.Utils;
    public Schema outputSchema(Schema input) {
        try {
            String schemaString = "ScoreBoard:Tuple(Name:chararray, Score:int)";
            return Utils.getSchemaFromString(schemaString);
        } catch (Exception e) {
            return null;
        }
    } 

Call "DESCRIBE" in pig and we see the result as: 

    #!java
    A: {ScoreBoard: (Name: chararray,Score: int)}