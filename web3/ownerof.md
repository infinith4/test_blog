```
import { ethers } from "ethers";

const provider = new ethers.JsonRpcProvider("https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID");
const contractAddress = "0xYourNFTContractAddress";
const tokenId = "12345"; // Token ID

const abi = [
    "function ownerOf(uint256 tokenId) external view returns (address)"
];

const contract = new ethers.Contract(contractAddress, abi, provider);

async function getOwner() {
    try {
        const owner = await contract.ownerOf(tokenId);
        console.log("Owner Address:", owner);
    } catch (error) {
        console.error("Error fetching owner:", error);
    }
}

getOwner();
```
