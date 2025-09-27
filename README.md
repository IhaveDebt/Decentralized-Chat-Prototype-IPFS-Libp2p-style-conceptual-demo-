/**
 * Decentralized Chat Prototype (p2p_chat_stub.ts)
 *
 * This stub demonstrates the messaging flow you'd implement with libp2p/IPFS.
 * It simulates peers sending messages into a shared "gossip" store.
 *
 * Usage: ts-node src/p2p_chat_stub.ts
 */
type Message = { id: string; from: string; text: string; ts: number };
const gossipStore: Message[] = [];

function peerSend(peer: string, text: string) {
  const m: Message = { id: `${Date.now()}:${Math.random().toString(36).slice(2)}`, from: peer, text, ts: Date.now() };
  gossipStore.push(m);
  console.log(`[${peer}] sent: ${text}`);
}

function peerReceive(peer: string) {
  const unseen = gossipStore.slice(-10); // naive
  console.log(`[${peer}] sees ${unseen.length} messages`);
  unseen.forEach(m => console.log(`  ${m.from}: ${m.text}`));
}

// Demo
peerSend('alice', 'Hello peers');
peerSend('bob', 'Hi alice');
peerReceive('carol');
